# Git

Git is a [Version Control System](Glossary#Version%20Control%20System). It's built to let people work on the same project at the same time, while also not being reliant on an internet connection. 

Git has many tools, but the basic usage is very simple.

## Git Terminal

### Adding Changes to Git

To add your code changes to Git, use the following commands:
```bash
git add .
git commit -m "Write a short summary of what your changes do"
git pull
```

#### Merge Errors

At this point, Git might detect a **merge error**. If someone has been working on the same files as you, then you'll need to select which changes to keep and which ones to discard. A merge error will output something like this:
```
Automatic merge failed; fix conflicts and then commit the result
```

Try building your project. Some files will have errors. Go to those files and make sure that they're correct. Once you've fixed all of the merge errors, `add`, `commit`, and `pull` again:

```bash
git add .
git commit -m "Fix merge errors"
git pull
```

Then, you can `push` to finish the upload process!

```bash
git push
```

#### No Merge Errors

If you *don't* have a merge error, you can enter this command to upload the changes to GitHub. After this, then you're done!

```bash
git push
```


### Getting Up-to-Date from Other People

Downloading up-to-date code is extremely simple. You can do it in just *one command*.

```bash
git pull
```

However, if you've been working in the same files as others, you may need to commit first. Git will tell you if you need to do this; just enter the following commands:

```bash
git add .
git commit -m "Write a short summary of what your changes do"
git pull
```

#### Resetting

Sometimes, you don't care about *your* changes, and you just want to download the newest version. There's a command for resetting the repository so you can download changes easily!

```bash
git reset --hard HEAD
git pull
```

### Checking Out Previous Versions
In Git, you can see *every* previous version, no matter who made it. As long as you've used `git pull`, you can see past commits with `git log`.

That will show you something like this:
```
commit bb0262d991e3bcf9ceb5498e4df35a805fbb9cd7 (HEAD -> master, origin/master, origin/HEAD)
Author: coleh <coleh@coleh.net>
Date:   Tue Oct 12 21:28:48 2021 -0400

    Fix error when trying to hash empty directory

commit eb058f13615018979f13ed96ca44e39130fa7b36
Merge: a82c855 fa2caae
Author: shaashwat <shaash317@gmail.com>
Date:   Tue Oct 12 20:00:02 2021 -0400

    resolve merge

commit a82c855ba9364b2a1710c82c543c8a2540f3dcc7
Merge: 4bb44c3 1d99848
Author: shaashwat <shaash317@gmail.com>
Date:   Tue Oct 12 19:56:47 2021 -0400

    tried optimizing code

commit fa2caaeb03045b23443c07457fa02e1f2bf0b230
Author: Duelephant <pmb221@students.needham.k12.ma.us>
Date:   Tue Oct 12 19:07:36 2021 -0400

    test teleop
```

**Because showing every commit at once is too much, Git uses a "pager" program. Different computers have different pagers; press "h" to see how to use yours.**

After you've found the commit that you want to inspect, copy the twenty-digit [commit ID](Glossary#Commit%20ID) and enter `git checkout <the ID>` to load it. 

Once you're done with the commit, use `git checkout master` to go back to the future.


## GitHub Desktop