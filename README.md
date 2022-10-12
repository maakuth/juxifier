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
- Current guidance: is the pump allowed to run now

## Outputs
- Boolean value: should the pump be allowed to run right now?

## Building blocks

### Cooling estimator
A function that takes the temperature history and determines the rate of that the accumulator is cooling.
This is used to determine the time until the accumulator cools down to the minimum acceptable temperature.

### Heating governor
Let the pump run if the power at present hour is cheapest available before hitting the minimum

### Something with inertia
The heating governance should not be changing all the time.
If the power cost at now + 2h is cheaper than now, should we only let the pump run until it's barely warm enough to not hit the minimum?
Perhaps the correct thing to do is to only run seldom enough that it's not an issue if the pump only runs for the duration between two iterations.
