# Model assumptions and configured inputs

This document distinguishes **verified model settings** from assumptions that still need justification.

## Verified configured inputs

| Item | Current model value |
|---|---:|
| Model time unit | Minute |
| Delivery-truck interarrival time | 1 hour |
| First truck arrival | At model start |
| Delivery-truck movement speed | 40 km/h |
| Pallets created per unloading truck | 60 |
| Forklift capacity | 5 |
| Forklift speed | 1 m/s |
| Pre-CNC stochastic delay | Triangular(15, 20, 30) min |
| CNC processing delay | 1 min |
| Raw-material storage | `warehouse_storage` |
| Storage type | Selective rack storage |
| Forklift home area | `forkliftParkin` |
| CNC home locations | `nodeCNC1`, `nodeCNC2` |

## Important modelling assumptions to justify

The model file tells us what values are configured, but it does **not by itself establish why those values are realistic**.

The final portfolio should therefore explain the source of:

1. the 1-hour truck interarrival time;
2. the batch size of 60 pallets;
3. the five-forklift capacity;
4. the triangular 15/20/30-minute delay;
5. the 1-minute CNC processing time;
6. the available CNC capacity;
7. storage dimensions/capacity;
8. travel speeds and spatial layout.

For each, classify the source as one of:

```text
Tutorial specification
Measured / real data
Literature
Modelling simplification
Analyst assumption
```

## Current evidence status

At present these values should be presented as **model configuration**, not validated real-world manufacturing data.

That distinction should remain explicit in any GitHub, LinkedIn or CV description.
