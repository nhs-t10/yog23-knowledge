# Git

Git is a version control system. It's built to let people work on the same project at the same time, while also not being reliant on an internet connection. 

Git has many tools, but the basic usage is very simple.

## Git Terminal

To add your code changes to Git, use the following commands:
```bash
git add .
git commit -m "Write a short summary of what the changes do"
git pull
```

### Merge Errors

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

### No Merge Errors

If you *don't* have a merge error, you can enter this command to upload the changes to GitHub. After this, then you're done!

```bash
git push
```


## GitHub Desktop