# Job Shop Manufacturing Simulation — AnyLogic

A portfolio case study documenting a **Job Shop manufacturing and material-handling simulation built in AnyLogic 8.9.9**.

The repository is being developed as an engineering and operations-analysis portfolio project rather than simply as a tutorial upload.

## Model status

The actual `Job Shop.alp` file has now been reviewed.

Verified model metadata:

- **AnyLogic version:** 8.9.9
- **Model name:** Job Shop
- **Java package:** `job_shop`
- **Model time unit:** minutes
- **Modelling approach:** discrete-event process flow with Material Handling and 3D/network markup
- **Main entity types:** `Pallet` and `Truck`
- **Resource-unit types:** `ForkliftsTruck` and `CNC`

The repository documentation below is based on the actual model file rather than guessed architecture.

## Operational problem represented

The model links inbound delivery trucks, pallet unloading, raw-material storage, forklift handling, CNC processing and final completion.

A useful portfolio question is:

> How do inbound delivery timing, warehouse handling, forklift capacity and CNC processing interact to determine production flow, congestion, resource utilisation and throughput?

## Verified model architecture

### Delivery-truck flow

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

The delivery-truck source is configured with:

- interarrival time: **1 hour**;
- first arrival: **at model start**;
- initial location: `exitNode`;
- speed: **40 km/h**.

`drivingToDock` sends trucks to `receivingDock`.

`unloading` is a manual Delay at `receivingDock`. When a truck enters unloading, it executes:

```java
sourcePallets.inject(60);
```

This creates **60 Pallet agents** for that delivery.

After unloading completes, trucks move back to `exitNode` and leave through `sink1`.

### Pallet / production flow

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

Key verified settings:

- `sourcePallets` is a **manual Source** creating `Pallet` agents at `receivingDock`.
- `storeRawMaterial` stores pallets in `warehouse_storage` using the `forklifts` ResourcePool.
- `warehouse_storage` is a selective rack-storage area.
- `delay` uses `triangular(15, 20, 30)` minutes.
- `seizeCNC` seizes a unit from the `cnc` ResourcePool.
- `retrieveRawMaterial` retrieves material using the `forklifts` ResourcePool.
- `processing` uses a **1-minute** processing delay.
- `releaseCNC` releases the CNC resource.
- `sink` removes completed Pallet agents from the process.

## Verified resources

### Forklifts

`forklifts` is a ResourcePool with:

- capacity: **5**;
- custom resource-unit type: `ForkliftsTruck`;
- speed: **1 m/s**;
- home node: `forkliftParkin`.

The forklifts are used by both `storeRawMaterial` and `retrieveRawMaterial`.

### CNC resources

`cnc` is a ResourcePool using the custom resource-unit type `CNC`.

Its capacity is defined by home locations:

```text
nodeCNC1
nodeCNC2
```

The production flow seizes a CNC resource before retrieval/processing and releases it afterward.

## Material-handling and spatial model

Verified markup includes:

- `warehouse_storage` — rack storage;
- `receivingDock` — area node;
- `forkliftParkin` — area node;
- `exitNode` — truck-network point;
- `nodeCNC1` and `nodeCNC2` — CNC locations;
- `network` — movement network;
- multiple 3D cameras.

This makes the project suitable for both operational analysis and visual portfolio evidence.

## Important interaction between the two flows

The truck and pallet processes are coupled.

When a delivery truck reaches `unloading`:

```java
sourcePallets.inject(60);
```

creates the pallet batch.

The storage block contains this exit action:

```java
if( self.nWaitingForResource() == 0 )
    unloading.stopDelayForAll();
```

This links completion of pallet storage with release of the manually delayed unloading truck when no pallet is still waiting for a required resource.

That interaction is one of the strongest pieces of logic to explain in the portfolio.

## KPIs to add next

The current model file does not contain a finished KPI dashboard, so the next development stage is instrumentation.

| KPI | Why it matters | Suggested visual |
|---|---|---|
| Throughput | Completed pallets per run/time unit | KPI + time plot |
| Cycle time | End-to-end pallet time | Histogram + mean |
| WIP | Pallets currently in the production system | Time plot |
| Forklift utilisation | Material-handling load | Bar chart |
| CNC utilisation | Processing-resource load | Bar chart |
| Queue/waiting before resources | Congestion and bottlenecks | Time plot |
| Storage occupancy | Warehouse loading | Time plot |
| Truck turnaround time | Inbound logistics performance | Histogram / KPI |

## Planned portfolio experiments

1. **Baseline** — current model.
2. **Higher delivery frequency** — reduce truck interarrival time.
3. **Larger/smaller batch size** — vary the 60-pallet injection.
4. **Forklift capacity** — compare fewer/more than five forklifts.
5. **CNC capacity** — vary the number of CNC resource locations/units.
6. **Processing-time change** — vary the 1-minute CNC processing time.
7. **Pre-processing delay variability** — alter the triangular 15/20/30-minute delay.

Each experiment should compare the same KPI set and use repeatable settings.

## Repository structure

```text
job-shop-manufacturing-simulation/
├── README.md
├── model/
│   └── README.md
├── images/
│   └── README.md
├── results/
│   ├── throughput/
│   ├── cycle-time/
│   ├── utilisation/
│   ├── queues/
│   └── scenarios/
├── docs/
│   ├── modelling-notes.md
│   ├── assumptions.md
│   └── validation.md
└── LICENSE
```

## Current next steps

1. Upload the real `Job Shop.alp` file into `model/`.
2. Add a full AnyLogic model screenshot.
3. Add a 3D runtime screenshot.
4. Add a close-up showing storage/forklift/CNC material flow.
5. Instrument throughput, cycle time, WIP and utilisation.
6. Run the baseline.
7. Run controlled capacity/demand scenarios.
8. Add result charts and interpretation.

## Attribution

The model originated through AnyLogic learning/tutorial work and is being developed into a portfolio case study through model understanding, debugging, documentation, KPI instrumentation, experimentation and analysis.

Third-party tutorial content, software, trademarks and assets remain the property of their respective owners.
