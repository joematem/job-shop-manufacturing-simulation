# Scenario results

This folder will store controlled experiment comparisons.

Initial experiment framework:

| Scenario | Possible change |
|---|---|
| Baseline | Existing configuration |
| Higher demand | Increase arrival rate |
| Added capacity | Add/increase processing capacity |
| Added handling capacity | Increase transport/material-handling resources |
| Faster processing | Reduce processing time |
| Failure/disruption | Introduce downtime if model supports it |
| Buffer change | Increase/decrease intermediate capacity |

Each scenario should ideally be compared using the same KPI set:

- throughput;
- cycle time;
- WIP;
- queue length/waiting;
- utilisation;
- bottleneck location.

Recommended outputs:

```text
scenario-summary.csv
scenario-comparison.png
scenario-analysis.md
```

The exact scenario definitions will be revised after the real model is reviewed.
