# PR PlayGround - Talent Boost Academy (2022)
Practise Submitting and Updating PRs
>This repository could be used as a reference. \
No-judgement, it is ok to make mistakes

## What you will learn?
- How to contribute to open source projects
- How to maintain your fork
- How to update your PR 
- How to resolve conflicts raised in your PR
 
## Configure your git
Before you do anything, set up your gitconfig - set your username and email
INFO: the username and the email will be visible in any commits you push to GitHub from the command line. If you'd like to keep your real name private, you can use any text as your Git username.

```
$ git config --global user.name "YOUR_NAME"
$ git config --global user.email your_name@mail.com
```
## Fork the project you want to contribute to 
Most commonly, forks are used to either propose changes to someone else's project or to use someone else's project as a starting point for your own idea.
Forks are often used in open source development on GitHub. When you contribute in open source project you may not 
have permission to do commits in the original repository. So you need to fork it. By forking a repository, you are 
creating a copy of the repo to your account.


##Submit PR from your fork

### Clone your fork
```
$ git clone <your clone>
$ cd puns
```
### Configuring a remote for a fork
```
$ git remote add upstream https://github.com/ORIGINAL_OWNER/ORIGINAL_REPOSITORY.git
$ git remote -v
```
### Fetch the remote repo 
```
$ git fetch upstream
$ git checkout -b work-to-submit upstream/master
```
### Do your changes and commit them
```
$ git add <files>
$ git commit -s
```
It is time to think for a good commit message

```
Commit message title; Max 50 charachters

Wrap the body at 72 characters
Separate the subject from the body with a blank line
Use the body to explain what and why vs. how

Signed-off-by: Diana Atanasova <dianaa@vmware.com>

```

### Push your change into your fork

```
$ git push origin work-to-submit
```

### Create a Pull Request (PR) 
By opening a pull request you propose to the upstream repository the changes you've made to your fork.
With your PR you ask collaborators for feedback on your changes. So be prepared to receive comments and address them.
1. Navigate to the original repository where you created your fork.
2. Above the list of files, click "Pull request".
3. Validate if the "base repository" & "head repository" are correct. Head is your repository where you have done 
   your changes. Base repository is the upstream repo. Took a look if the branches are also correct.
4.Type a title and description for your pull request.
   
<b>[TODO] ADD VIDEO ?</b> 

## How to update your GitHub fork to get new changes from the original project

Assuming you have no new local changes: when you run `git status` you should not see files modified or staged for commit.

```
$ git pull --rebase
```

But what if you do have files that are modified? Use the `git stash` to save your changes.

```
$ git stash push
$ git pull --rebase
$ git stash pop
```

## How to update your commit with changes to files
The maintainer of the original project asks you to make some changes to your PR. You've gone ahead and made the changes to the files. Now:

```
$ git add <files>
$ git commit --amend
```

Make changes to the commit message if you need to.

```
$ git push -f origin work-to-submit
```

Your PR will be automatically updated.

*HOLD UP!* Did someone tell you `-f` or force push was bad? Forced updates on your own fork when nobody else is working on it is fine. If you mess up you can still pull changes from upstream and start fresh. But remember, *never* `git push -f upstream`!

## How to add a Signed-off-by to your commit message
A Developer Certificate of Origin (DCO) is required in your commit message. If you have set up your gitconfig, this is easy. Do:

```
$ git commit --amend -s
```

Check your commit message. Once saved:

```
$ git push -f origin work-to-submit
```

Your PR will be automatically updated.

## How to resolve conflicts in your PR



## How to combine two or more commits into one (squash)
Sometimes, the maintainer will ask you to change something in your commit, and you may instead add another commit to your PR (maybe you didn't know about force pushes). The maintainer may then ask you to squash your commits, that means combining your commits into one big commit (we won't go into reasons why a maintainer may as you to do this - there are several reasons why). This is where `git rebase -i` helps:

```
$ git rebase -i HEAD~<count from HEAD to the first commit on your PR branch>
```

For example, you submitted 3 commits in your PR. To squash all 3 you can run:

```
$ git rebase -i HEAD~3
```

Running this will open up your default editor. It will show something like this:

```
pick 4e9a282 Added bark pun to dogs <-- first commit
pick ae74d75 Added sniffing pun to dogs <-- second commit
pick 3344294 Added howl pun to dogs <-- third commit

# Rebase eb0ef4c..3344294 onto eb0ef4c (3 commands)
#
# Commands:
# p, pick <commit> = use commit
# r, reword <commit> = use commit, but edit the commit message
# e, edit <commit> = use commit, but stop for amending
# s, squash <commit> = use commit, but meld into previous commit
# f, fixup <commit> = like "squash", but discard this commit's log message
# x, exec <command> = run command (the rest of the line) using shell
# b, break = stop here (continue rebase later with 'git rebase --continue')
# d, drop <commit> = remove commit
# l, label <label> = label current HEAD with a name
# t, reset <label> = reset HEAD to a label
# m, merge [-C <commit> | -c <commit>] <label> [# <oneline>]
# .       create a merge commit using the original merge commit's
# .       message (or the oneline, if no original merge commit was
# .       specified). Use -c <commit> to reword the commit message.
#
# These lines can be re-ordered; they are executed from top to bottom.
#
# If you remove a line here THAT COMMIT WILL BE LOST.
#
# However, if you remove everything, the rebase will be aborted.
#
# Note that empty commits are commented out
```

To combine all 3 together, change the second and third commit to `squash`. Then save the file via your text editor.

```
pick 4e9a282 Added bark pun to dogs
squash ae74d75 Added sniffing pun to dogs
squash 3344294 Added howl pun to dogs
```
   
You should get something like this:

```
# This is a combination of 3 commits.
# This is the 1st commit message:

Commit message 1

Signed-off-by: Diana Atanasova <dianaa@vmware.com>

# This is the commit message #2:

Commit message 2

Signed-off-by: Diana Atanasova <dianaa@vmware.com>

# This is the commit message #3:

Commit message 3

Signed-off-by: Diana Atanasova <dianaa@vmware.com>

# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
```

As the message says - anything with `#` at the beginning will be ignored. So imagine your commit message looking like this:

```
Commit message 1

Signed-off-by: Diana Atanasova <dianaa@vmware.com>

Commit message 2

Signed-off-by: Diana Atanasova <dianaa@vmware.com>

Commit message 3

Signed-off-by: Diana Atanasova <dianaa@vmware.com>
```

You probably want to make this more readable. After editing, save using your text editor. Now you can resubmit your PR:

```
$ git push -f origin work-to-submit
```

## How to undo your commits
If you want to undo your commits while still keeping the changes to your files:

```
$ git reset HEAD~<count commits from tip of working branch to the last commit you want to undo>
```

For example, you want to undo the last commit you made on the branch, do:

```
$ git reset HEAD~1
```

*What is this HEAD?* HEAD points to the tip of your current working branch. Run `git log` to quickly get your bearings. HEAD will be the first commit that comes up.

## How to move your commit to another branch on upstream


## How to make your master catch up with upstream's master


