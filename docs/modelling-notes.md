# Modelling notes

## Purpose

This document will record how the Job Shop simulation actually works.

At this stage, the repository structure is prepared, but the real model file/screenshots have not yet been reviewed here. Therefore exact block names, machine names, routing rules and parameters are deliberately not invented.

## Information to extract from the real model

When the `.alp` file or clear screenshots are provided, document:

### System entities
- What enters the model?
- Is the entity called Product, Job, Part, Order, Pallet or something else?
- Are there multiple job/product types?

### Process route
Record the exact sequence of blocks.

Example format only:

```text
Source
  ↓
Queue
  ↓
Machine / Service
  ↓
Transport
  ↓
Next process
  ↓
Sink
```

Replace this with the actual process.

### Processing resources
Record:

- machine/workstation names;
- number of units;
- processing-time logic;
- resource pools;
- setup/changeover logic if present;
- failure/downtime logic if present.

### Material handling
If used, record:

- forklifts;
- transporters;
- conveyors;
- pallets;
- storage;
- network paths;
- movement destinations.

### Queues and buffers
For each important queue:

- location;
- capacity;
- what causes waiting;
- which downstream resource releases the queue.

### Custom logic
Record any:

- variables;
- parameters;
- functions;
- events;
- statecharts;
- Java expressions;
- routing conditions;
- custom agent types.

## KPI instrumentation plan

### Throughput
Create a counter or use sink statistics for completed jobs/products.

### Cycle time
Store entry time on each entity and calculate:

```java
time() - agent.entryTime
```

at completion.

### WIP
Measure the number of jobs/products currently inside the manufacturing system.

### Queue length
Use numeric queue statistics from the relevant blocks.

### Utilisation
Measure the busy fraction for the actual ResourcePool/machine resources used.

## Experiment discipline

For each scenario:

1. change only the intended parameter/resource configuration;
2. retain the same simulation horizon where appropriate;
3. document random-seed/replication handling;
4. use multiple replications for stochastic comparisons where practical;
5. compare the same KPIs;
6. do not interpret animation alone as performance evidence.

## Portfolio principle

The final README should distinguish:

- what the tutorial originally provided;
- what was fixed/debugged;
- what was extended;
- what was measured;
- what was experimentally tested;
- what conclusions are supported by the results.
