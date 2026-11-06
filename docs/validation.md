# Verification and validation

## Verification status

The `.alp` file has been structurally reviewed.

Verified process connections include:

### Truck flow

```text
sourceDeliveryTrucks
→ drivingToDock
→ unloading
→ drivingToExit
→ sink1
```

### Pallet flow

```text
sourcePallets
→ storeRawMaterial
→ delay
→ seizeCNC
→ retrieveRawMaterial
→ processing
→ releaseCNC
→ sink
```

The model also contains the expected referenced resources and spatial objects:

- `forklifts`;
- `cnc`;
- `warehouse_storage`;
- `receivingDock`;
- `forkliftParkin`;
- CNC nodes.

## Logic checks to perform in AnyLogic runtime

Structural inspection does not replace runtime verification.

The next verification run should check:

1. A truck is generated at the beginning of the run.
2. New trucks arrive at approximately the configured 1-hour intervals.
3. Each truck reaches `receivingDock`.
4. Entering `unloading` injects exactly 60 pallets.
5. Pallets are stored using forklift resources.
6. The truck is released from manual unloading only when the intended storage condition is satisfied.
7. Pallets pass through the triangular delay.
8. CNC resources are seized before processing.
9. Raw material is retrieved with forklift resources.
10. Processing lasts the configured 1 minute.
11. CNC units are released after processing.
12. Completed pallets reach `sink`.
13. Trucks return to `exitNode` and reach `sink1`.
14. Counts reconcile: created pallets = pallets in system + completed pallets, subject to any explicitly removed entities.

## Validation status

The model configuration has **not yet been validated against real manufacturing data** in this portfolio.

Possible validation approaches:

- tutorial/reference-behaviour comparison;
- face validation;
- extreme-condition testing;
- conservation/count checks;
- comparison with expected throughput;
- sensitivity analysis;
- comparison with real or published manufacturing data if later available.

## Experiment credibility

Before using this portfolio to make operational claims:

- record simulation run length;
- document random seed handling;
- use replications for stochastic results;
- define any warm-up period;
- calculate uncertainty/confidence intervals where appropriate;
- keep scenario changes controlled;
- separate animation evidence from statistical performance evidence.

## Current portfolio claim

At this stage, it is defensible to say:

> The model architecture and configured process logic have been reviewed and documented.

It is **not yet defensible** to claim:

> The model has been validated as a representation of a real manufacturing system.

That stronger claim requires evidence beyond the `.alp` structure.
