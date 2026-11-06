# Job Shop Manufacturing Simulation — AnyLogic

A portfolio case study for a **Job Shop manufacturing simulation developed in AnyLogic**.

The purpose of this repository is to document the model as an engineering and operations-analysis project rather than simply as an AnyLogic tutorial exercise.

## Project objective

The portfolio will show how the model represents production flow through a manufacturing system and how simulation can be used to study:

- throughput;
- cycle time;
- work in process (WIP);
- queues and waiting;
- machine/resource utilisation;
- material-handling performance;
- bottlenecks;
- capacity changes;
- disruption and scenario performance.

## Current portfolio status

This repository has been created as the portfolio shell.

**Not yet uploaded / verified**

- the real AnyLogic `.alp` model;
- exact model process-flow architecture;
- final machine/resource configuration;
- 2D/3D model screenshots;
- measured KPI results;
- scenario experiment outputs.

These items will be added only from the actual working model and simulation runs.

## Portfolio question

A useful central question for this project is:

> How do processing capacity, material-handling resources and demand interact to determine throughput, cycle time, queueing and congestion in a Job Shop manufacturing system?

This question may be refined once the real model configuration is reviewed.

## Intended KPI dashboard

| KPI | What it measures | Intended visual |
|---|---|---|
| Throughput | Jobs/products completed | KPI / time plot |
| Cycle time | Time from system entry to completion | Histogram + mean |
| Work in process | Jobs currently in the system | Time plot |
| Queue length | Congestion before workstations | Time plot / bar chart |
| Waiting time | Non-processing delay | Histogram / summary |
| Machine utilisation | Busy versus available capacity | Bar chart |
| Material-handling utilisation | Use of forklifts/transport resources if present | Bar chart |
| Storage occupancy | Use of buffers/storage if present | Time plot |
| Idle time | Unused machine/resource capacity | Bar chart |
| Bottleneck | Resource restricting flow | Scenario comparison |

## Planned experiments

The exact experiments will depend on the real model, but the initial portfolio framework is:

| Scenario | Change | Question |
|---|---|---|
| Baseline | Current configuration | How does the system perform now? |
| Higher demand | Increase arrivals | Where does congestion appear? |
| Extra processing capacity | Add/increase a machine resource | Does throughput improve? |
| Extra material handling | Add/increase transport capacity | Is movement a bottleneck? |
| Faster processing | Reduce processing time | Does the bottleneck move elsewhere? |
| Resource failure | Introduce downtime where applicable | How resilient is performance? |
| Buffer/storage change | Alter intermediate capacity | Does blocking or waiting change? |

No scenario result will be claimed until it is generated from the model.

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
│   │   └── README.md
│   ├── cycle-time/
│   │   └── README.md
│   ├── utilisation/
│   │   └── README.md
│   ├── queues/
│   │   └── README.md
│   └── scenarios/
│       └── README.md
├── docs/
│   ├── modelling-notes.md
│   ├── assumptions.md
│   └── validation.md
└── LICENSE
```

## Evidence needed to complete this portfolio

The next evidence to add is:

1. **Actual AnyLogic model file** — the working `.alp` project.
2. **Model overview screenshot** — full process logic visible.
3. **3D/animation screenshot** — full running Job Shop environment if the model has 3D.
4. **Process-flow screenshot** — close view of the main production blocks and routing.
5. **Resource/machine screenshot** — the important machine, processing or material-handling area.
6. **Dashboard screenshot** — after KPIs are added.
7. **Measured result exports** — after baseline and scenario experiments are run.

## Development stages

```text
Working model
    ↓
Document actual architecture
    ↓
Instrument KPIs
    ↓
Build dashboard
    ↓
Run baseline experiment
    ↓
Run controlled scenarios
    ↓
Compare results
    ↓
Interpret bottlenecks and trade-offs
    ↓
Complete GitHub case study
```

## Tools and methods

Planned documentation will cover the tools actually used in the model, potentially including:

- AnyLogic 8.9.9 PLE
- Discrete-event simulation
- Process Modelling Library
- Material Handling Library, if used
- Resource pools
- Queues and buffers
- Java expressions/functions
- Events and agent logic
- 2D/3D animation
- AnyLogic Analysis charts

Only features present in the real model will be described as implemented.

## Attribution

If the original Job Shop was developed from AnyLogic learning/tutorial material, the final case study will state this transparently and distinguish:

- the original learning model;
- modifications and debugging;
- KPI instrumentation;
- scenario experiments;
- performance analysis;
- independent extensions.

Third-party tutorial content, software, trademarks and assets remain the property of their respective owners.
