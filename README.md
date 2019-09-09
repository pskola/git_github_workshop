# 1. Setting up git
## 1.1  Download git

* Mac Users: https://git-scm.com/downloads
* Windows User: https://github.com/git-for-windows/git/releases/tag/v2.23.0.windows.1
	

## 1.2 Configuring git 
This user name and email will be associated with your subsequent Git activity, which means that any changes pushed to GitHub, BitBucket, GitLab or another Git host server in a later lesson will include this information.

### Setup username and email
> git config --global user.name "Your Name"

> git config --global user.email "Your Email"


### Setup the correct linebreaks encoding depending on your OS
**Mac/Linux**
> git config --global core.autocrlf input

**Windows**
> git config --global core.autocrlf true

### Setup "nano" as the text editor to interface with git
> git config --global core.editor "nano -w"

#### Helpful links to setting up git 
https://help.github.com/en/articles/configuring-git-to-handle-line-endings#platform-all



# 2. Creating a Repository (`git init`)
## 2.1 Create a directory in your Desktop for this workshop
```
cd ~/Desktop
mkdir workdir
cd workdir	
```

## 2.2 Create a repository, where git store versions of your file
```
git init
```

Check that a hidden folder `.git` has been created
> ls -a 

Check the status of git
> git status

# 3. Tracking Changes (`git add & commit`)

## 3.1 Adding new files/modification to staging area (`git add`)
Make sure you are in the correct directory
> cd ~/Desktop/workdir

Make a new file `foo.txt`
> touch foo.txt

Check the status
> git status

If there are **untracked files**, we would like to add those files so git will track their changes:
> git add foo.txt

Check the status again, `foo.txt` should now be ready to get committed (a commit is a revision to your files).
> git status

## 3.2 Saving these changes to the repository (`git commit`)

Commit the file and note the identifier for this commit (e.g., `f22b25e`):
> git commit -m "Add foo.txt to repo"

What have we done so far? Lets check the log, which list all the commits made so far. 
> git log

## BONUS - Checking what has changed before add/commit (`git diff`)
Add some text to the file `foo.txt`
> echo hello >> foo.txt

Check what has changed between your last commit and now:
> git diff

Add & commit your changes to `foo.txt`
> git add foo.txt

> git commit -m "Add hello in foo.txt"

Check the status and log again (`git status` and `git log`)

###  Notes

* Git does not track an empty directory, so until a directory has a file in it, git would not track it. 
* `git add` adds file to a **staging area**, and `git commit` save these changes in the staging area to the repository.



# 4. Exploring History (`git diff & show`)
## 4.1 Difference between current file and N commit ago (`git diff HEAD`)
Lets add another line to `foo.txt`
> echo world >> foo.txt

Check what is different from your current version of foo.txt compare to the last commit
> git diff HEAD foo.txt

Check difference compare to two commits ago
> git diff HEAD~1 foo.txt

Check difference against a specific commit based on identifer (the unique identifier is different for you, use `git log` to check!)
> git diff 7be71q foo.txt 

## 4.2 What was done in ____ commit? (`git show`)
Sometimes we want to check what was done during a certain commit (instead of comparing differences)
> commit show HEAD~1 foo.txt

# 5. Reverting to a previous commit (`git checkout`)
## 5.1 Going back to a specific version of a file (`git checkout`)
Before going back to a previous state of a file, COMMIT what you have now
> git add foo.txt

> git commit -m "Add world"


Recover the `foo.txt` that doesn't have "world" in it (use HEAD~1 or unique identifier)
> git checkout HEAD~1 foo.txt

Check what is in `foo.txt`
> cat foo.txt

Go back to the state where "world" was in the file
> git checkout HEAD foo.txt


## 5.2 Going back to an entire commit - Detached HEAD (CAUTION)
If you `git checkout` a previous commit without also specifying a file, you will revert the entire directory to a previous condition
> git checkout HEAD~1 

You should get a message like this
```
You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by performing another checkout.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -b with the checkout command again. Example:

 git checkout -b <new-branch-name>
```

Use `git checkout HEAD` to return to most recent state. IF you git chekcout a previous commit without commit your current state, then anything not commited would be lost!!!
