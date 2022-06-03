# Updating the FTC SDK

This **must** be done by the Software Manager after the Kick-Off Event. It **may need** to be done before competitions.

1) Find the SDK Github for this year. It's usually under https://github.com/FIRST-Tech-Challenge -- the current GitHub is <https://github.com/FIRST-Tech-Challenge/FtcRobotController>. 
2) Copy the URL.
3) Run the following commands in a terminal. If you *aren't* using Android Studio, make sure to `cd` into the repository's folder.
	```bash
	git remote add ftc [enter the URL here]
	
	# This may cause merge errors. If it does, accept them and continue.
	git pull ftc master --allow-unrelated-histories
	```
4) Build the project. **There are usually merge errors.** For each error, fix it by accepting the *incoming* change (the *second* code block in the `<<<<` *code* `=====` *code* `>>>>>` sequence)
5) Re-build. There may still be errors! If there are, fix them on a case-by-case basis.
6) Once builds are successful, apply the Autoauto installation patches as documented in [how-the-compiler-works](../autoauto/how-the-compiler-works.md).


This updates the Robot Controller. You might also need to follow [preparing-or-upgrading-phones](preparing-or-upgrading-phones.md) to update the Driver Station.
