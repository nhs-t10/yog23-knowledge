# Roadrunner Manager
Created by @achyutS1281
## General Overview
`RoadRunner Manager` is Manager for Road Runner!

![Duh! Image](https://media.tenor.com/SKdBU2zjlywAAAAM/duh-well.gif)

You may be asking, "What is RoadRunner?"

`roadrunner` is a path and trajectory following algorithm that takes control of the robot in order to follow precise paths that you can specify

Of course, you can see how this would benefit our auto. There would be no more square paths, it would be solely curves and coordinated movements to take advantage of a chassis' speed and capabilities.

The best way to specify paths is using YAML files, but you can use other methods in this manager in order to create your own path on the fly...

In this .md file, you will learn everything about `RoadRunnerManager` and how to best follow paths efficiently

## How to set up a RoadRunnerManager in your TeleOp

First up, you need to pass in your `hardwareMap`

This is usually already defined as long as your teleop extends `opMode` or `LinearOpMode`

Next, you need a start pose...

To do this, you can say:

```new Pose2d(x, y, Math.toRadians(heading))```

Remember that `x` and `y` can be from -72 to 72 and that the axes are switched when looking at the field from the audience's point of view. When looking from this pint of view, positive x means up, negative x means down, positive y means left and negative y means right.

Next up, we need to pass in the `TelemetryManager` 

You should have a `TelemetryManager` in your opMode for displaying relevant metrics

Simply declare the object and pass in the variable into the constructor.

Then, just type in `this` for the next parameter. This will tell the manager which opMode is calling it. Finally, if you are using RR for teleop, put true in this next parameter. If not, put false.

And That's It!

Here is a sample constructor call for reference (in Auto, not TeleOp): ```rr = new RoadRunnerManager(hardwareMap, new Pose2d(0, 0, Math.toRadians(0)), telemetryManager, this, false);```

