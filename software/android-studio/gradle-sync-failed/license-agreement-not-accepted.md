# Gradle Sync Failed: License Agreement Not Accepted

This error happens when you're installing a new version of Android. It is characterized by the following text in the build log:

```
Failed to install the following Android SDK packages as some licenses have not been accepted.
```


**This is an easy error to fix.**

First, look in the build log. There is a line that says "_Android SDK Platform \<a number\>_". Remember the number-- that's your **API Level**. 

Second, go to the preferences:

![Error](https://raw.githubusercontent.com/nhs-t10/yog22-knowledge/master/software/android-studio/gradle-sync-failed/Pasted%20image%2020211014133125.png)

and select **Appearance & Behavior** > **System Settings** > **Android SDK**.

![Settings](https://raw.githubusercontent.com/nhs-t10/yog22-knowledge/master/software/android-studio/gradle-sync-failed/Pasted%20image%2020211014133311.png)

This data table will have all up-to-date versions of Android. Make sure that the row with your _api level_ has its checkmark checked, and hit "Apply".

That will open a wizard which walks you through the solution. In ninety-nine percent of cases, this will fix the problem.
