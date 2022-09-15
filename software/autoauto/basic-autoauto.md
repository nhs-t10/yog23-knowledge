# What is Autoauto?

Autoauto is a custom programming language made by [chloe](https://github.com/chlohal). It is *built for auto!* 

With Autoauto, you don't have to deal with huge switch/case statements or weird workarounds for sensors. You can just code :)

**Note:** Lines are referred to as states interchangably throughout the guide, as Autoauto works as a finite state machine.

## How to Code in Autoauto

An Autoauto program is structured like this:

First, a statepath is created using hashtag (#) followed by the name of the statepath, and then a colon (:). Usually the first statepath of an Autoauto program will be `#init:`.

With this new statepath, you can begin to write proper autoauto code. You can either begin executing code in #init, or you can jump to another statepath using `goto` followed by the name of the statepath you wish to jump to. Many autoauto programs use this to jump to a statepath that corresponds to the first autonomous objective. In theory, this second statepath could replace `#init:` if `#init:` is otherwise empty, but it doesn't really affect anything to include the initialization statepath, and is a good future-proofing technique.

In most autonomous programs, moving the robot is essential. This can be done using `driveOmni` in the exact same way as a TeleOp program! Then, on the same line, use an `after` statement to tell the robot when it should move on to the next instruction. Valid measurements include units of time such as seconds and milliseconds, as well as units of distance such as inches, centimeters, and rotational degrees. You can actually create two after statements, and the state will advance when one is completed, though it doesn't matter which one. Following the after statement, include a `next;` to tell the robot to move to the next state. An example of a driveOmni instruction in Autoauto would look like this: `driveOmni(0.5,0,0), after 2in next;`.
**Note:** Make sure that at the end of your program, you set all motor powers to 0. 

It's likely that you won't only need to drive around during the autonomous period. When you need to move motors that are not related to driving, you can use `setMotorPower()`, including the name of the motor in quotation marks, followed by the power you wish to give the motor. Similar to driving, follow this up by an `after` statement, and then a `next` statement. Moving a motor in autonomous would look something like this: `setMotorPower("Carousel", 0.5), after 3000ms next;`.
**Note:** Be sure to set the power back to 0 in the next statement, otherwise the motor will continue moving at the previously given speed!

Variables are fairly important in many programs, and Autoauto programs are no exception. In order to make a variable, use the `let` method. Setting a variable in autonomous would look like this `let variable = 5`. After this, you can include a timed delay, or immediately move on to the next statement. 

Trying to program an autoauto movement but you can't quite get some timings right? Use the `when` statement to wait until a certain value reaches a certain point, such as a movement being completed. An `when` statement would look something like this: `when (hasEncodedMovement("ClawMotor") == false)`. 

Looking for conditionals? You can use if statements in a similar way to in TeleOp! You can include more than one on the same line if the contained code is a single statement, which looks like this: `if(value == 0) goto thirdPosition, if(value == 1) goto secondPosition, if(value == 2) goto firstPosition`.

Debugging autonomous can sometimes be frustrating, but the `log()` method is here to help! Throw this in combined with a `next` statement within some curly brackets {}, and it can print text to the phone similar to a telemetry statement in TeleOp. An example of `log()` in Autoauto would look something like this: `{ log("movement done"), next };`

If you want to skip over some states, you can use a `skip` statement instead of a `next` statement, specifying how many statements you want to skip over. You can also skip backwards, though *be careful* when doing so, as you can create infinite loops and get easily stuck. An example of a `skip` statement in Autoauto would look something like this: `skip 2;`, or `skip -2;`. 
