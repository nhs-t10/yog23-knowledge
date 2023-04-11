# ManipulationManager

## ManipulationManager Overview

`ManipulationManager` is the main manager for controlling motors and servos that are not the driving motors.

Those should only be used by `MovementManager`, since `ManipulationManager` lacks integration with our omniDrive code.

To initialize a `ManipulationManager`, use a template similar to this: 

```
hands = new ManipulationManager(
                hardwareMap,
                crservo         (),
                servo           ("monkeyHand"),
                motor           ("monkeyShoulder")
        );
```
        
Insert the list of names as they're specified in your phone's configuration. If they're at all different, the code motors and servos won't find their physical counterpart and give errors. 

## ManipulationManager Functions

Here are some of the most important functions for `ManipulationManager`:

### SetServoPosition
Takes in a position as a double from 0 to 1 and a string name and runs the servo by that name to that point. If the name isn't in the list of servos, it'll throw an exception.

### SetServoPower/SetMotorPower
Takes in a string name and double from 0 to 1 and sets the servo or motor by that name to the specified power.

### GetMotorPower/GetServoPower
Takes the motor or servo power at a specified name and returns it as a double. Useful for telemetry.

### GetMotorPosition
Takes the current encoder position at a specified name and returns it as a double. Useful for telemetry. 

### GetServoPosition
Takes the servo position from 0 to 1 and returns it as a double. Useful for telemetry.

### SetMotorModes
Sets all motors to the specified mode.

### SetMotorMode
Sets the named motor to the specified mode.

### SetZeroPowerBehavior
Sets the named motor to the specified zero power behavior.

### EncodeMoveToPosition
Moves a specified motor to the specified encoder position.
