# First Commit

If you're here, you've downloaded the code and built it!! Now, it's time to upload your own changes.

The [build history monitor](../autoauto/build-history/about-the-build-history-monitor.md) will have made a few changes for you, so we'll upload those in this document.

## Getting Permissions for your GitHub Account

If you don't have a GitHub account, go to <https://github.com/join> to make one. Give your username to a [github admin](../people-to-ask-about-things/github-admin.md) and ask them to [add you to the GitHub organization](adding-someone-to-github.md).

## Adding GitHub account to your Git 

Your GitHub account is created, but your computer's `git` installation doesn't know about it. If you tried to upload, this would cause an error!

First, we need to make sure that `git` knows your username and email. These will be applied to each upload you make, and they make sure that your GitHub account gets linked to them.

Enter the following commands into a terminal; replace `USERNAME` with your GitHub username and `EMAIL` with the email you used for GitHub.

```bash
git config --global user.name "USERNAME"
git config --global user.email "EMAIL"
```

You've now *logged in*, but you haven't *authenticated* (provided your password). We'll do that in the "Push" step.

## Status, Add, and Commit

> ⚠️ GUIs (**graphical** user interfaces; click-button-and-enter-text) exist for Git. This guide *exclusively* uses the CLI (**command line** interface; enter-commands). If you would prefer to use a GUI, feel free, but they are *not* covered in this. 
> For more info, see [why-cli](../git/why-cli.md)

Git is great. It lets you upload any changes you like, with a **commit message** to summarize what those changes are!

Enter the terminal command `git status` to see which files you've edited. Even if you haven't edited anything, your [build history](../autoauto/build-history/about-the-build-history-monitor.md) file will have been added.

Right now, the files are "unstaged"-- they will *not* be uploaded in your next commit. To add them to the stage, enter `git add .`. If you want to be more precise, you can use `git add [FILE]`, where `[FILE]` is one of the files listed in `git status`.

Enter `git status` again after adding. You'll notice that the files have been added to the staging area! 

Use the command `git commit -m "[MESSAGE]"` to package the file changes into a "commit", which can be uploaded. Replace `[MESSAGE]` with a short summary of your changes-- for your first one, you can use `initial commit`.

Great job! :) If you have any problems at this step, call your Software Manager over to help.

## Push (Upload)

### Authenticate with GitHub

Authenticating your terminal with GitHub requires a PAT (Personal Access Token). You can make one by following the [official instructions here](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token#creating-a-token)

**Recommendations**
- Either make your PAT have *no expiry* (you can always revoke it later), or have it expire *after you graduate from high school.*
- Give your PAT the `repo` permission, as well as all permissions *under* `repo` 

After you've gotten your token, paste it into a Doc or somewhere where you can keep it safe. We'll save it in Git, but for now, you need to keep it on hand.

To make sure that Git saves your login, enter this command:
```bash
git config --global credential.helper store
```
*Note: this saves your PAT on-disk*

Now, enter `git push` to upload your committed changes! This will prompt you for your **username** and **password**. 

> 🔴 If `git push` doesn't ask for your login, then someone else has used your computer and you should log them out! 
> You can Google 'git credential store erase' for this, since methods wildly vary by platform. However, a lot of people recommend unsetting `credential.helper`-- don't do that.

In the username prompt, enter your GitHub username. In the password prompt, paste your PAT. Instead of CTRL+V to paste, right-click and hit "paste". Make sure that you don't copy any whitespace (`PAT `   is different from `PAT`)

**Note that you will *not see your PAT being typed in.* This is a security feature-- just like how you see "\*\*\*" when typing a password on a website**.

This should successfully push to GitHub! In the future, you won't have to enter your PAT-- it's been saved on your computer.

