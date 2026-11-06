# AnyLogic model

The actual model supplied for this portfolio is:

```text
Job Shop.alp
```

It has been inspected and is an **AnyLogic 8.9.9** XML project.

## Verified model metadata

```text
Model name: Job Shop
Java package: job_shop
Model time unit: Minute
AnyLogic version: 8.9.9
```

## Verified custom agent/resource types

- `Pallet` — Material Item
- `Truck` — Entity
- `ForkliftsTruck` — Resource Unit
- `CNC` — Resource Unit

## Verified main blocks

```text
sourcePallets
storeRawMaterial
delay
seizeCNC
retrieveRawMaterial
processing
releaseCNC
sink

sourceDeliveryTrucks
drivingToDock
unloading
drivingToExit
sink1

forklifts
cnc
```

## File still needed in GitHub

The real `.alp` file has been provided in the ChatGPT workspace and reviewed, but it still needs to be added to this GitHub folder as the actual project file.

Upload it here as:

```text
model/Job Shop.alp
```

Do not substitute a recreated or placeholder model.
