# Git & Github Notes

- Git is a version control system (VCS) that manage versions of source code, also known as a source code manager (SCM).

- Github is a distributed service that hosts Git projects. Don't initialize README.md if you already have existing files for a repository.

- **Repository** contains the project work, as well as few hidden files used to communicate with Git. A repository can either be local on your computer of remote on someone else's computer.

- **Local working directory** are the files in your compute's file system. It is not the same as files saved (committed) in the repository. When working with Git, the working directory is different than the command line's concept of "current working directory."

- **Command line's working directory** refers to the directory  that your shell is looking at.

- **Staging area** is a space/file in the Git directory that stores information about what will go into your next commit.

- **SHA** (secure hash algorithm) is an ID number for each commit, consisting of a 40-character string.

- **Commits** are snapshots of the current state of the project. It is the fundamental unit of Git.

- If you're in a directory that is a Git repository, the command prompt will include the name of the branch in parentheses.

- Create a `.gitignore` file to add names of the files that you want Git to ignore and not add to the staging area.

- A Github repository stores metadata, which is hidden in `.git` file. Use `ls -a` to see the hidden files. Hidden filed get transferred when you clone a repository.

- `git config --global color.ui auto` gets colored output on the Terminal.

- `diff -u <old-file-name> <new-file-name>` shows the difference in changes between the two files.

## Log

`git log` shows every commit that has been made. Use `j` or the down-arrow to scroll down, `k` or the up-arrow to scroll up, and `q` to quit the log. Only shows commits of the branch you're current in/checked-out.

`git log --stat` shows statistical information of commits.

`git log --oneline` shows SHA and commit messages only.

`git log -p` shows the actual changes made in the files changes, rather than just the statistics.

`git log -p <first-7-characters-of-SHA>` shows commits starting at that specific SHA commit and prior.

`git log --oneline --decorate --graph --all` shows commits of all the branches. `--graph` adds bullets and lines to visualize the "branching" and `--all` shows all the branches in the repository.

`git log --graph --oneline master <branch-name>`

`git show` shows the same information as `git log -p` and `git show <SHA>` shows the changes of that specific commit.

`git log` and `git show` will only show changes that were committed.

## Diff

`git diff` with no arguments will show the changes between the working directory and the staging area. Only `git diff` shows changes even before they're committed.

`git diff --staged` shows the changes between the staging area and the repository.

## Branch

Branch is a line of development created to diverge from the main line (master) of development.

`git branch` shows all branches of the repository. the `*` tells you which branch you're current in/checked-out.

`git branch <new-branch-name>` creates a new branch named, <new-branch-name>. When you create a new branch, it will have all the existing commits from the master branch.

`git branch <new-branch-name> master` crates a branch ahead of the master branch, resulting in a fast-forward merge. Don't include `master` if you want to diverge from the master branch.

If you have a new feature and want to share with collaborators but not jeopardize the master branch, create a new branch, add, commit, and `git push origin <new-branch-name>` not master!

`git branch -d <branch-name>` deletes that specified branch. Use after the branch has been merged into master. You can't delete the branch while you're in it so checkout to master first. Use `-D` to force the delete.

## Checkout

Checkout is when content of the repository has been copied to the working directory.

`git checkout <branch-name>` Changes between branches. Checks out that specified branch.

`git checkout -b <new-branch-name>` runs `git branch` and `git checkout` at once.

`git checkout -b <new-branch-name> master` creates a new branch, checks out that specified new branch, and starts it at the same location as the master branch. Any changes here will be "ahead" of the master branch. If merged, it will be a fast-forward merge. If you `git log --decorate` and see `(HEAD -> <branch-name>, master)`, it means that the specified branch is on the same and latest commit as the master branch.

## Tag

`git tag -a <flag-name>` "flags" a commit so they stand out from the rest (e.g., v.1.0 or beta).

`git tag <flag-name>` has no `-a`. `-a` means annotated flag. Annotated flags are recommended because they include more information like author, date, and message of tag.

`git tag` shows and verifies the created tag. Using `git log --decorate` will show the newly created tag with its associated commit.

`git tag -d <flag-name>` deletes the tag.

`git tag -a <flag-name> <SHA>` tags an older commit.

## Revert

`git revert` reverts/undos a specific commit (i.e., if characters were added, Git reverts by removing the characters and committing). `git revert <SHA-of-commit-to-revert>`

## Reset

`git reset` erases commits but not recommended. Use with caution. You can use `git reflog` to recover something you reset within 30 days. `git reset <SHA-of-commit-to-reset>`

Use `git reset --hard HEAD^` if you made the wrong merge and need to undo the change. `^` means "relative commit reference" and indicates the "parent commit."

`--mixed` is the default option for `git reset`. It will move the commit to the working directory. `--soft` moves the commit to the staging area. `--hard` moved the commit to the trash.

`^` refers to the parent commits (e.g., `HEAD^`, `HEAD~1`).

`~` refers to the grandparent commit (e.g., `HEAD^^`, `HEAD~2`, and not `HEAD^2`). Great-grandparent commit works the same (e.g., `HEAD^^^`, `HEAD~3`, and not `HEAD^3`).

There is a difference between `^` and `~`. A merged branch will have two parents. That's why `^` used with number cannot reference the parent. Only more of the `^` symbol will work. `^` will refer to the first parent of the commit. `^2` will refer to the second parent of the commit.

`git branch backup` creates a backup of the branch.

## Amending a Commit

`git commit --amend` edits (create a new commit and replace) the most recent commit. You can use this command to add forgotten files. Re-add and re-stage the new files and run `git commit --amend` instead of `git commit`.

## Creating a Remote Repository

1. `git init` initializes an empty Git repository. If it's a brand new repository, there is no HEAD yet because there is no commit yet.

2. `git remote add origin <url-from-github>`. `git remote` links your local repository to an online/remote repository (i.e., establishing a connection with Github).

3. `git remote` shows the origin. `git remote -v` shows the verbose path. If you `git remote` your local repository, there will be no information. But if you `git remote` a cloned repository, it shows "origin" or whatever name you gave it. This is the location of the remote repository. `git remote -v` shows the full path of the repository.

4. `git status` shows the status of changes. Also, shows the files that available to add and commit. The files moved to the staging area will appear in green. Files with changes that have not added to the staging area yet will appear in red.

5. `git add <name-of-file>` adds that specified file to the staging area. Use `git add *` to all all files in the current directory.

6. `git commit` opens up Sublime (setting configured in .bash_profile) to add a commit message on line 1. Write commit message as a command, in present tense and first word capitalized (e.g., Change color of header in index.html). Or to not prompt Sublime, use `git commit -m "<commit-message>"`.

7. `git push <destination> <branch-name-that-contains-commits-you-want-to-push>` which most likely translates to `git push origin master`. This pushes the local files to the master branch on the remote repository. Use `git push -u origin master` the first time you push to simply run `git push` in the future.

8. `git log` shows the history of commits.

## Cloning a Remote Repository

`git clone <url-from-github>` clones an existing repository. Use `git clone <url-from-github> <name-name>` to rename the repository instead of using the default one.

After cloning a repository, you can use `git shortlog` to see all commits, sorted by author's name alphabetically. Use `-s` and  `-n` together to see the number of commits by each author and sorted by the number of commits, respectively.

To filter by author's name, use `git log --author=Dani` or use `git log --author="Dani Kim"`.

Other filtering options are `git show <SHA>` or grep, which is a pattern matching tool by `git log --grep="Hello"` Same as `git log --grep=Hello`.

## Pulling Changes to Local Repository

After cloning, if the remote repository gets modified by collaborators, pull in the latest commits.

1. `git pull` gets your local master up to date with the remote master.

`git pull origin master` runs `git fetch origin` and `git merge master origin/master` at once.

2. Use `git log` to see all the new commits made by others.

Be careful when pulling repositories because it will overwrite existing files on the local master. To avoid this overwrite, fetch the files instead.

`git fetch` fetches the most recent commits and will become/names, origin/master. `git fetch origin master` will fetch the changes from the remote repository but does not sync with origin/master. To sync, use `git merge origin/master`.

## Merging

`git merge` combines Git branches.  Git will take the branches it will merge, look in their history to find the single commit that both branches have, combine the lines of code that were changed on the separate branched, and commit to record the merge. Use `git merge <branch--name-to-merge-into-current-branch`.

When merging, you have to be in/checkout the branch and you will merge another branch *into* the current/checked out branch.

It is important to know which branch you're on when merging branches. Merging makes a commit.

If the branch is ahead of the master branch, it will be a fast-forward merge. When one commit is reachable/has access to the master branch, it is ahead. You will know the branch is ahead of the master if you run `git log --oneline --graph --decorate --all`.

1. To merge two divergent branches, make sure you're in the master branch.

2. `git merge <branch-name-to-merge-into-master-branch>` prompts Sublime with a default commit message. Save and close Sublime.

3. When merged into the master branch, that is the end of that branch's life, so you can delete that branch.

When resolving a merge conflict, open up the file in conflict by `subl <name-of-file>`.
`<<<` is the head, with my changes. `===` is the common ancestor, with the original source code. `---` is the collaborator's code. Make the changes and delete the special characters. Use `git status` to check that both have been modified.

## Pushing Local Commits to Remote Repository

`git push <destination> <branch-name-that-contains-commits-you-want-to-push>` which most likely translates to `git push origin master`.

The branch that appears in the local repository is always tracking a branch in the remote repository. This copy is called, origin/master. If you make changes on your local directory, origin/master will be out of date. At this point, you can't pull from the remote repository because your local files will be overwritten.

1. To sync the remote repository, run `git fetch origin master`. When fetched to local machine, that copy will be named, origin/master.

2. Checkout master branch to merge another branch into master. Then, run `git merge origin/master`. This will merge the fetched copy (origin/master) with the master branch on your local machine.

3. Push your local master branch into your remote repository, known as origin by `git push origin master`. This will get your remote repository up to date.

## Forking

Forking makes an identical copy and you become the owner of that copy. Different than cloning. Cloning duplicates a remote repository to your local machine. Forking duplicates a remote repository by creating a new remote repository on my Github. You cannot push to a cloned repository if you don't own it. You don't have access to it.

1. To make changes and push commits, first fork the remote repository.

2. `git clone <url-from-github>`

3. After making changes on your local machine, you can use `git diff` before committing to see the differences.

4. Run `git add` and `git commit`.

5. `git push origin master`. Or use `git push origin <branch-name>` you're pushing a branch. Make sure that the branch's name is topical.

Enter Github username and password when prompted.

## Pull Request

1. Fork the repository on Github.

2. `git clone <url-from-github>`

3. After making changes on your local machine, run `git add` and `git commit`.

4. `git push origin master` to forked repository.

6. Create a pull request on Github for the topic branch.

## Upstream

When you fork someone's (e.g., Dani's) remote repository, you can clone it to your local machine to modify it. While doing so, Dani's repository get updated. Dani's repository is considered the "upstream." To get Dani's update repository, use `git pull upstream master`.
