# InputManager

## General Overview

`InputManager` is the manager that handles inputs! (Shocker, I know). 

The primary reason that we want to use `InputManager` instead of just reading the gamepad data directly is because of `InputNodes`.

These are the minions of `InputManager` and they help us speed up our TeleOp code. 

`Nodes` run in our "inputs" (which are not the same as the gamepad data, we just named them in a silly way), and each "input" has a thread of its own, meaning that they can all run concurrently.

This allows us to take processes, boolean checks, mathematical operations, and other more complex tasks out of the process of our loop, reducing the iteration time of each loop.

The reason we do this is to make the controls more efficient and have reduced input lag, which makes the robot feel more responsive and controllable, and also cause it's cool ;).

## Setting Up InputManager

First, you need to declare an InputManager in your TeleOp. You can check the javadoc comments for information on how to do this by hovering over the name and pressing ctrl+Q.

However, I'm going to explain it here anyway, to make this a one stop shop for InputManager.

Step 1: Make sure your TeleOp imports `InputManager`. (`import org.firstinspires.ftc.teamcode.managers.input.InputManager;`)

Step 2: Create a new InputManager just like any other java object before the `init()` function.

Step 3: Inside the `init()` section of your TeleOp, initialize the `InputManager` with both gamepads as parameters. (`input = new InputManager(gamepad1, gamepad2);`)

Step 4: Call your inputManager's `.registerInput()` function in order to declare inputs! `.registerInput()` requires a `String` parameter as the name of the input.

Step 5: Use Nodes as you need them for the input. A good place to start are the `JoystickNode` and `ButtonNode`, which take the basic stick and button data, respectively, from the gamepad and convert it into data that is useable by other Nodes. If you're not sure what Nodes you might want to use, check out the Nodes guide below!

Step 6: Use your input in `loop()` as needed (often as a condition for an if-statement). Depending on what output your input gives, you might want to use `.getBool()` (for buttons), `.getFloat()` (for sticks), or `.getFloatArrayOfInput()` (driveOmni likes to have a float array so outputting a float array from your input is useful for that)

Step 7: Once your input is read, perform whatever tasks are nessecary with that data, whether it be running functions, turning motors or servos, toggling variables, etc. Congrats! You successfully implemented `InputManager` into your TeleOp code!
