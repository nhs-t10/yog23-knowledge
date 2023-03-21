# InputManager

## General Overview

InputManager is the manager that handles inputs! (Shocker, I know). 
The primary reason that we want to use InputManager instead of just reading the gamepad data directly is because of InputNodes.
These are the minions of InputManager and they help us speed up our TeleOp code. 
Nodes run in our "inputs" (which are not the same as the gamepad data, we just named them in a silly way), and each "input" has a thread of its own, meaning that they can all run concurrently.
This allows us to take processes, boolean checks, mathematical operations, and other more complex tasks out of the process of our loop, reducing the iteration time of each loop.
The reason we do this is to make the controls more efficient and have reduced input lag, which makes the robot feel more responsive and controllable, and also cause it's cool ;).