# Preparing Next Year's Repository 

The Software Manager should do this *early* in the post-season every year.

## The Easy Way and The Other Way

### Using the GitHub Template Feature

This is the easiest way to do it. If GitHub ever removes Templates or puts them behind a paywall, skip to the next section.

Otherwise:

First, make the **current year**'s repository into a template. The [official documentation](https://docs.github.com/en/repositories/creating-and-managing-repositories/creating-a-template-repository) has the easiest way to do that.

Then, follow [Github's documentation on making the next year's repository from that template](https://docs.github.com/en/repositories/creating-and-managing-repositories/creating-a-repository-from-a-template). Make sure that the next-year repository goes in the **organization** (`nhs-t10`); not your personal account. It must be public so that people can pull without logging in. Check the "Include all branches" box (this isn't *super* important, but it's good to have).

Repositories should be named like the [Naming section](#Naming) documents.


### Using Git and Basic Transfer

If you've used the GitHub Templates feature successfully, then skip this section.

Otherwise:

[Make a new repository with the GitHub documentation](https://docs.github.com/en/repositories/creating-and-managing-repositories/creating-a-new-repository). Create it in the `nhs-t10` organization, *not* your personal account Follow the [Naming section](#Naming) for names. Don't add a README or a gitignore: you need a fully blank repo. Once you're done, copy the new repository URL.

Go into the *current year*'s repository on your *local* computer.  Make sure that the command line says "Robotics_20XX_20YY" on it! (If you're using the Android Studio terminal, that's the default). Enter the following terminal command to remove the git records

*Windows*
```cmd
rd /s /q .git
```

*Mac/Linux*
```bash
rm -rf .git
```

Then, initialize a *new* git local repo:

*All platforms*
```
git init
git add .
git commit -m "initial commit"
```

and upload it to the GitHub repo you made.

*All platforms*
```
git remote add origin [URL of new repository]
git push -u origin master
```

### Repo Naming 

Repositories should be named like this: `Robotics_20XX_20YY`, where `20XX` and `20YY` are the two years that the school year covers. For example, the 2022-2023 season uses `Robotics_2022_2023`

If making a repository for another team, prefix with a short abbreviation. For example, `LO2_Robotics_20XX_20YY` or `HH_Robotics_20XX_20YY`.

## Archiving and Moving People Over

After the initial transfer, it's a pain to have work moved. To make sure that nobody pushes work to the **current year**'s repository, make it **archived**. Follow [GitHub's official documenation](https://docs.github.com/en/repositories/archiving-a-github-repository/archiving-repositories) to do that.

Then, have everyone follow [from-boot-to-build](from-boot-to-build.md), starting from *Cloning the Repository*, to swap over to the new repo.


