# MovementManager

## MovementManager Overview

`MovementManager` is the main manager that we use to control the four driving motors on a standard chassis. 
If you plan to use a non-four wheel chassis, don't expect everything in here to work perfectly, as it's not designed for that.

Typically, we call the four motors `fl, fr, bl, br`, which represents the front left, front right, back left, and back right motors, respectively.

To declare a `MovementManager`, you'll need to create four `Motor` objects directly from the hardware map like this:
`DcMotor fl = hardwareMap.get(DcMotor.class, "fl");`, changing the name for each motor. 
Then, feed them into the `MovementManager` constructor *specifically* in the order of fl, then fr, then bl, then br. This order is commonly used throughout `MovementManager` 
If you give it the wrong order, things won't work as expected. 
Alternatively, you could give it the hardware map directly, but you'll need to make sure that there are motors named fl, fr, bl, and br, and that they correspond to the correct motors on the robot.

## MovementManager Functions

Here, I'm going to list the most important functions from `MovementManager`.

### DriveRaw

A simple function that takes in four float values and sets the fl, fr, bl and br motors to those powers (in that order).
While this can be used manually, it's sometimes tricky to calculate these values by hand, and it's most often used while passed through a different function to calculate said float values automatically.

### DriveBlue

This is similar to `driveRaw`, but it also takes the robot's `Configuration` into account, so it knows what motor coefficients and motor reversals to use. 
For more information on the `Configration`, see `FeatureManager`.

### StopDrive

This will set all driving motor powers to 0 when called, useful for ensuring you're parked in AutoAuto.

### DriveOmni

This is the most important function in all of `MovementManager`, and it will be the main function you use to contol the robot's movement in every `OpMode`. 
It takes in three values, which represent the vertical, horizontal, and rotational components of the robot's movement, ranging from -1 to 1.
These can be input either as three floats or a float array of length 3.
It then takes these values and converts them to a float array of length 4, representing the specific motor powers of the drive motors, using a function called `omniCalc` in `PaulMath`, which was created by Paul Braverman who graduated in 2022.
Please don't mess with this function, as it'll break all of your drive code.
After this, it feeds the new float array into `driveBlue` to get the robot to run. 

### GetFL/FR/BL/BRMotorPower

These functions return the float value of their respective motor power from -1 to 1.

### ResetEncoders

Resets the ticks on all four of the robot's driving motors to 0 by setting them to the `STOP_AND_RESET_ENCODER` `RunMode`.

### RunToPosition

Sets the `RunMode` of all of the driving motors to `RUN_TO_POSITION`.

### RunUsingEncoders

Sets the `RunMode` of all of the driving motors to `RUN_USING_ENCODER`.

### RunWithOutEncoders

Sets the `RunMode` of all of the driving motors to `RUN_WITHOUT_ENCODER`.

### SetTargetPositions

Takes in four `ints` and sets their respective motor's target position to that int. If the motors are not in `RUN_TO_POSITION` mode, this won't do anything. 
