# Verification and validation

This document will record evidence that the Job Shop model behaves as intended.

## Verification — did we build the model correctly?

Checks should include:

- all process-flow connections work;
- agents/products have the correct type;
- resources seize and release correctly;
- queues behave as intended;
- transport/movement completes;
- no unexpected null references occur;
- no empty-collection/index errors occur;
- no disconnected ports remain;
- model counters reconcile with flow where possible.

## Validation — is the model a reasonable representation of the intended system?

Depending on the project stage, validation may use:

- tutorial/reference behaviour;
- face validation;
- extreme-condition tests;
- conservation checks;
- comparison with expected throughput;
- comparison with real or literature data if available;
- sensitivity analysis.

## Experiment credibility

Before interpreting scenarios:

- define the baseline;
- use consistent KPIs;
- document simulation time units;
- document run length;
- document stochastic distributions;
- use replications where appropriate;
- separate measured results from illustrative examples.

Actual validation evidence will be added after the working model is reviewed.
