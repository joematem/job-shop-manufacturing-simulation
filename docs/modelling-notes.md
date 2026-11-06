# Modelling notes

## 1. Model identity

The actual `Job Shop.alp` file has been inspected.

- AnyLogic version: **8.9.9**
- model time unit: **Minute**
- package: `job_shop`

## 2. Agent and resource types

### Pallet

`Pallet` is configured for Material Handling flow as a **MATERIAL_ITEM**.

It represents the raw-material/product unit moving through storage and CNC processing.

### Truck

`Truck` is an **ENTITY** used in the inbound delivery flow.

### ForkliftsTruck

`ForkliftsTruck` is a **RESOURCE_UNIT** used by the `forklifts` ResourcePool.

### CNC

`CNC` is a **RESOURCE_UNIT** used by the `cnc` ResourcePool.

## 3. Delivery flow

```text
sourceDeliveryTrucks
        ↓
drivingToDock
        ↓
unloading
        ↓
drivingToExit
        ↓
sink1
```

### sourceDeliveryTrucks

Verified settings:

```text
arrival type: interarrival time
interarrival time: 1 hour
first arrival: at start
location: exitNode
speed: 40 km/h
agent type: Truck
```

### drivingToDock

Destination:

```text
receivingDock
```

### unloading

This is a manual Delay located at `receivingDock`.

On enter:

```java
sourcePallets.inject(60);
```

Plain English:

> Each arriving delivery truck creates a batch of 60 pallet agents.

Because the Delay is manual, the truck does not leave simply because a fixed unloading time expires. Another piece of logic must call its stop-delay API.

### drivingToExit

Destination:

```text
exitNode
```

The truck then leaves through `sink1`.

## 4. Pallet / production flow

```text
sourcePallets
      ↓
storeRawMaterial
      ↓
delay
      ↓
seizeCNC
      ↓
retrieveRawMaterial
      ↓
processing
      ↓
releaseCNC
      ↓
sink
```

### sourcePallets

- agent type: `Pallet`
- source mode: manual
- location: `receivingDock`

Its normal creation mechanism in this model is:

```java
sourcePallets.inject(60);
```

from the truck-unloading process.

### storeRawMaterial

This Material Handling `Store` block uses:

```text
resource pool: forklifts
storage: warehouse_storage
```

On exit:

```java
if( self.nWaitingForResource() == 0 ) 
    unloading.stopDelayForAll();
```

Operational meaning:

1. a pallet finishes the Store block;
2. the Store checks whether any pallet is still waiting for a required resource;
3. if none are waiting, all trucks currently held in the manual `unloading` Delay are released.

This is the synchronization logic connecting the pallet-handling flow to the delivery-truck flow.

### delay

Delay time:

```java
triangular(15, 20, 30)
```

with time unit minutes.

So the delay is stochastic:

- minimum: 15 min;
- mode: 20 min;
- maximum: 30 min.

### seizeCNC

Seizes one unit from:

```text
cnc
```

### retrieveRawMaterial

Uses:

```text
resource pool: forklifts
destination node: forkliftParkin
```

This block retrieves the material from storage with forklift resources.

### processing

Processing delay:

```text
1 minute
```

### releaseCNC

Releases the CNC resource seized earlier.

### sink

Completed pallets leave the process through `sink`.

## 5. Forklift resource

`forklifts` ResourcePool:

```text
capacity: 5
resource-unit type: ForkliftsTruck
speed: 1 m/s
home node: forkliftParkin
```

The pool is referenced by:

- `storeRawMaterial`;
- `retrieveRawMaterial`.

This makes forklift utilisation a natural portfolio KPI.

## 6. CNC resource

`cnc` is a ResourcePool with custom unit type `CNC`.

Its capacity definition is based on home locations:

```text
nodeCNC1
nodeCNC2
```

This establishes two explicit CNC resource locations in the spatial model.

## 7. Storage and network

Verified markup:

```text
warehouse_storage — selective RackStorage
receivingDock     — RectangleNode
forkliftParkin    — RectangleNode
exitNode          — PointNode
nodeCNC1          — PointNode
nodeCNC2          — PointNode
network           — movement network
```

The model also contains multiple paths/nodes and three 3D camera objects.

## 8. Existing analysis

The supplied model does not currently contain a completed chart/dashboard layer.

Therefore portfolio analysis still needs to be added rather than reported as if already present.

## 9. Recommended measurements

### Throughput

Count pallets leaving `sink`.

### Pallet cycle time

Store model-entry time on each `Pallet`, then measure:

```java
time() - agent.entryTime
```

at completion.

### Truck turnaround time

Measure from `sourceDeliveryTrucks` creation until `sink1`.

### WIP

Track pallets that have entered but not yet reached `sink`.

### Forklift utilisation

Use the `forklifts` ResourcePool utilisation/statistics API.

### CNC utilisation

Use the `cnc` ResourcePool utilisation/statistics API.

### Queue/resource waiting

Measure waiting around Store/Retrieve/CNC acquisition where the model develops congestion.

## 10. Experiment candidates

Model parameters already provide meaningful experimental levers:

- truck interarrival time — currently 1 hour;
- pallet batch size — currently 60 per truck;
- forklift capacity — currently 5;
- CNC capacity/location count;
- triangular delay — currently 15/20/30 minutes;
- processing time — currently 1 minute.

## 11. Portfolio interpretation

The strongest story is not simply “I animated a job shop.”

It is:

> An inbound logistics flow releases pallet batches into warehouse storage; forklift resources execute material handling; pallets compete for CNC capacity; stochastic delay and resource constraints determine production performance. The simulation can then be instrumented to identify bottlenecks and test capacity/demand scenarios.
