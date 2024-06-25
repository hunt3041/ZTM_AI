# This is a guide to using Git from command line

## Initial Setup
To setup a folder from an already published repository: `git clone <URL>`

## Pushing Changes
1. To get the status: `git status`
    
    This will show any differences between local repository and github repository.
2. Add any new files: `git add <FILENAME>`
3. Running `git status` should reflect changes made in step 2.
4. Commit changes: `git commit -m <MESSAGE>`
5. Finalize commits to github: `git push`

## Pulling Most Recent Version from Git
To pull from github: `git pull`

## Using Branches
* To see branches: `git branch`
* Publish new branch: `git branch new <BRANCH_NAME>`
* To switch branches: `git checkout <BRANCH_NAME>`
* To merge current branch with another: `git merge <BRANCH_NAME>`

