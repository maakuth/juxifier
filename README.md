# juxifier
_Cost-optimizing heat pump control_

The goal is to develop heat pump control algorithm that picks the most cost-effective periods of time to run the ground-source heat pump without compromising room temperature and warm water availability.

## Target environment
Target is to run this as a script in Home Assistant, controlling [pumpunjuksautin](https://github.com/zouppen/pumpunjuksautin).

## Inputs
- Wall clock time
- Warm water accumulator temperature history up to current moment
- Minimum acceptable temperature of the accumulator
- Total cost of electric power per kWh for next hours (8 hours at minimum)

## Outputs
- Boolean value: should the pump be allowed to run right now?

## Building blocks

### Cooling estimator
A function that takes the temperature history and determines the rate of the 
