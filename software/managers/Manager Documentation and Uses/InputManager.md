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

## List of Nodes and Their Uses

### AccelerationNode

Takes in an input and will gradually accelerate it up to its maximum value. For most purposes, `GradualStickNode` will prove equally or more effective (and that's what I'd recommend using), but this Node is being documented for historical purposes since it was the precursor to `GradualStickNode`.

### AllNode

Takes in a list of inputs, and checks if they are all `true`. If they are, the `AllNode` returns `true`. This is useful for creating specific button combos.

### AnyNode

Takes in a list of inputs, and checks if at least one of them is `true`. If one is, the `AnyNode` returns `true`. This is useful for checking if any of a set of inputs is activated, such as for preventing two conflicting motor movements from being triggered at once. 

### BothcelerationNode

Takes in an input and will gradually accelerate it up to its maximum value. After the input ends, it will gradually decelerate back to 0. For most purposes, `GradualStickNode` will prove equally or more effective (and that's what I'd recommend using), but this Node is being documented for historical purposes since it was another precursor to `GradualStickNode`.

### ButtonNode

A very simple node. Takes in the name of a button, and then outputs whether that button is pressed or not as a `boolean`. The full list of names can be found in the main file of `InputManager`.

### CallOtherInputNode

Calls for another `InputNode` to run. I can't give a specific use case for it, since I never ended up using it. If you find it useful though, the option is there.

### ComboNode

Similar to `AnyNode`, you can use this to create button combos. It takes in multiple inputs, and if they are all activated __in the right order__, then the Node will return `true`. Unlike `AnyNode`, the order in which the inputs are activated matters. Think of it as holding a button to change firing modes in a shooter. If you press shoot, then hold the change button, you shoot normally. If you hold the change button and then the shoot button, you'll shoot in the second firing mode.

### DecelerationNode

Takes in an input and will gradually decelerate it from its given value to 0. For most purposes, `GradualStickNode` will prove equally or more effective (and that's what I'd recommend using), but this Node is being documented for historical purposes since it was another precursor to `GradualStickNode`.

### DoubleClickNode

Checks if you activate an input twice in quick succession. The exact timing window is determined by a value in `FeatureManager`, called `DOUBLE_CLICK_TIME_MS`. Think of this as double tapping walk to run in a game like Kirby. If you haven't played a Kirby game, then go play one! I'd recommend Kirby's Return to Dream Land for the Wii or Switch, it's really fun. (Just not during robotics meetings ;))

### GradualStickNode

Takes a float value and gradually accelerates it to its maximum from a set minimum. When the associated input (likely a stick) is no longer active, it will gradually decelerate to 0. The most effective Node to use if you want a value to increase or decrease over time. 

### IfNode

Can run if statements (in theory), but we haven't used it this year and the last I heard, it didn't work. If you want to use it, please double check it works and/or fix it if needed. :D

### InputManagerInputNode

The big boss of all Nodes, they all get their basic properties from this one. If you want to learn more about how Nodes work, you can check here. However, I'd recommend against changing this node, since messing with it could break every other node.

### InputVariableNode

Takes in a variable and outputs it as a Node output. Some nodes don't like direct values, so if they want a node, use this to convert.

### InversionNode

Takes in an input and a boolean. If the boolean is true, the Node reverses the input. It's a fairly simple node allowing you to toggle between standard and inverse controls at the press of a button.

### JoystickNode

Another baseline node. Takes float values of stick positions from the gamepad data. Two joystick nodes are needed for both the X and Y components of a joystick.

### MinusNode

Takes in two inputs, and subtracts the second one from the first. A basic math node to take calculations out of loop.

### MultiInputNode

Takes in mutiple inputs and converts them into an array of inputs. Useful for combining drive values into a single array, instead of multiple floats.

### MultiplyNode

Takes in two inputs, and multiples them together. A basic math node to take calculations out of loop.

### OneOfNode

Takes in multiple inputs, and returns the first input that is nonzero. For this purpose, booleans are treated as 0 and 1. If you have multiple inputs with certain priorities, you might want to use this. 

### PlusNode

Takes in two inputs, and adds them together. A basic math node to take calculations out of loop.

### ScaleNode

An older version of `MultiplyNode`. For most purposes, `MultiplyNode` is the superior option, as it can be used with non-input values.

### StaticValueNode

Creates a static variable but in Node form, so it can be used by other Nodes.

### ToggleNode

Takes an input as a toggle and flips between returning true and false when the input goes from inactive to active.
