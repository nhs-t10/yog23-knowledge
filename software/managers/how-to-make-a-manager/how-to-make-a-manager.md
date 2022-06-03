# How to Make a Manager 

## Basic

1) Make a new package in the `managers` directory. Name it after your manager-- if you're making `SampleManager`, name it `sample`.
2) Make a new class inside the manager's package. It *SHOULD* (but not *MUST*) be named like `packageName + "Manager"`.
3) Make the class `extend FeatureManager`. You might have to use `ALT` + `ENTER` to import `FeatureManager`.

You're done! This is a simple manager. However, it can't do anything yet.

## Behaviour

Behaviour can be whatever you want. Take a look at things like `NateManager`, `ManipulationManager`, or `MovementManager` for examples.

Some good practices include:
- __Managers over Hardware__
	Instead of having your manager's constructor accept motors, try having it accept a `ManipulationManager`. See `NateManager` for example.
- __HardwareMap over Hardware__
	If you *need* direct motors, prefer taking a `HardwareMap` instead of individual motors. See `ManipulationManager` for an example.
	


## Autoauto Connection

You don't *have* to connect your manager to Autoauto. It's *recommended*, but not *required:* for example, there's `InputManager`, since there's no input.

Almost all managers *should* be connected to Autoauto.

To connect your manager:

1) Code the initialization in Teleop first. For example, `ManipulationManager`'s initialization looks like this:
	```java
	//in the class
	ManipulationManager hands;

	//in the init() method
	hands = new ManipulationManager(  
			hardwareMap,  
			crservo         (),  
			servo           ("servoName1", "servoName2"),  
			motor           ("motorName1", "motorName2", ...)  
	);
	```
	Coding in Teleop first lets you use autocomplete.
2) Go to `template.notjava`. It is usually in the `src/main/scripts/autoauto-compiler/compiler/data/` folder, but **use [double-shift](../../android-studio/keyboard-shortcuts.md) instead of trying to hunt for it**.
3) Add your initialization to the `template`, right before line 95. Make sure to also copy-paste any **import statements**, as they are **not** auto-added to `template.notjava`.
5) Add your manager's variable name to the `runtime = R(`*...*`);` line. This "gives" it to the Autoauto runtime.

**NOTE: If there are any syntax errors in Autoauto, FIX THEM IN `TEMPLATE.NOTJAVA`. FIXES IN THE AUTOAUTO CLASSES THEMSELVES *WILL* BE OVERWRITTEN**

After you've added it to `template.notjava`, all *autoautoable* methods will be automatically linked!!

A method is *autoautoable* if it:
- Doesn't use varargs
- Has primitives or `String`s for all of its arguments
- Returns a primitive or a `String`, or is `void`.


