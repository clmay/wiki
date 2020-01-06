## How to combine Git repos with full history

- [A note about conventions](#a-note-about-conventions)
- [Create an empty repository on GitHub](#create-an-empty-repository-on-github)
- [Prepare each old repository](#prepare-each-old-repository)
- [Consolidate the old repositories into the new one](#consolidate-the-old-repositories-into-the-new-one)
- [There's just one thing left](#theres-just-one-thing-left)

---

Prior to this semester, I had been keeping my code for every class in a separate
repository. This semester, I realized that adding another 4-5 repos to my GitHub
account for every term was probably a bad idea. I wanted to consolidate them all
into a single git repo, but I didn't know how to combine the repos and keep the
commit history for all of them separate repos. Since my GitHub activity consists
almost entirely of commits on schoolwork, I didn't want my contribution activity
to disappear when I deleted the old individual repos.

I did a bit of research, but most of the instructions were vague and unclear. I
came up with the steps below by synthesizing others, after a hefty dose of trial
and error. Now, my activity timeline on GitHub shows the exact same statistics
that it did before combining the repos. It may go against some git/GitHub best
practices, but for my purposes, it worked well enough.

### A note about conventions

Text within angle brackets (`<`, `>`) signifies content that needs to replaced
by some actual value. So `<url_to_new_repo>` literally means the URL for the new
repo. You'll want to copy and paste the commands from the tutorial, and then
remove the angle bracket bits and replace them with their corresponding values.

### Create an empty repository on GitHub

First, create an old repo on GitHub. Then, clone the empty repo && cd into it:

```sh
git clone <url_to_new_repo>
cd <new_repo_name>
```

Create an empty commit:

```sh
git commit --allow-empty -m "Initial commit"
```

The empty commit is important! Later steps will fail if GitHub does not detect a
new commit in the repo!

### Prepare each old repository

Note: this entire section deals with the **old repos**, not the new one.

Make a folder inside each of your other repos, at the top-level of each repo. In
Finder, press `Cmd+Shift+.` to show hidden files, and within each repo, move all
the files and folders (except for `.git/`) into the new folder. Maybe your
shell-fu is stronger than mine, but I found this easiest to do graphically,
using Finder. Make sure you don't move the `.git/` folder (leave it where it
is)! If you move it, things will break!

After you have finished moving the files out of the top-level (into the new
folders), commit the changes in each repo, and push them:

```sh
cd <path_to_old_repo>
git add .
git commit -m "Prepare for merge to <github_username>/<new_repo_name>"
git push origin master
```

Repeat for all of the repositiories that will be merged.

### Consolidate the old repositories into the new one

Note: you will be working in the **new repo** for the steps in this section.

The steps in this section can be completed either repo by repo (choose a repo,
complete steps 1–N, then the next repo, etc.) or you can complete each step for
every repo before moving on (step 1 for all repos, step 2 for all repos, etc.).
Whatever you find works best to make sure that all the steps get completed in
exactly the order they are listed (and none gets skipped).

1. First, get back into the new repo you created in the first section:

   ```sh
   cd <path_to_new_repo>
   ```

1. Then, create a remote for each of the old repos:

   ```sh
   git remote add <old_repo_name> <url_to_old_repo>
   ```

   The above step makes the new repo aware of the old repos.

1. Now that the remotes are added, fetch them to update the new repo with
   information about the old repos:

   ```sh
   git fetch --all
   ```

1. Then, create a branch for each of the old repos, using the old repo's master
   branch as a starting point:

   ```sh
   git checkout -b <old_repo_name> <old_repo_name>/master
   ```

   And then list the files to make sure everything is there:

   ```sh
   ls
   ```

   You should see all the files from the old repo. Assuming everything is
   showing up, you're ready to go back to the `master` branch and start merging
   the changes into it.

1. Go back to the master branch, and merge and commit each of the branches from
   the old repositories:

   ```sh
   git checkout master
   git merge --allow-unrelated-histories <old_repo_name> master -m "Merge <old_repo_name> branch"
   ```

1. Now that you've got everything from that repo merged into the new repo, it's
   time to do a little cleanup.

   ```sh
   git remote remove <old_repo_name>
   git branch -D <old_repo_name>
   ```

So far, so good. Those steps complete the process to merge a single old repo
into the new repo. Repeat for all of the repositiories that will be merged.

### There's just one thing left

Once you've completed the hard work above, you should be left with a single repo
that now has all the files, as well as the complete commit histories, of each of
the other repos that you merged into it. Time to push it up!

```sh
git push origin master
```

When you delete your old repositories from your GitHub account, your
contribution activity should remain unchanged!

---

[All tutorials](/tutorials.md)

#git #tutorials #system-administration #unix-like #original-content
