#### Standard initialisation:
```shell
git init #Create .git 
git remote add <Name> <URL> #Connect to repo
git add . #Stage all files
git commit -m "msg" #Commit staged files with message
git push <Name> <Branch> #Push files to a remote repo
```

___________
#### .gitignore boilerplate:
```shell
<raw relative path without quotes>
*.<extension> #all files with given extension
```
___________
#### Reseting the head/files:
```shell
git reset --hard #Reset branch to last commit
git reset --soft HEAD~1 #Reset to staging area
git restore --staged <File> #unstage
```
___________
#### Create and change branch:
```Shell
git branch <name> #Create branch
git checkout <name> #Switch branch
git merge <main> #Merge remote commits from a branch
```
#### Pull branch without losing uncommitted changes:
```shell
git stash 
git pull <branch>
git stash pop
```
___________
#### Avoiding merge conflicts:
```shell
git pull --rebase #Merge existing locally committed changes with remote changes
git pull --rebase=false #Do not merge local changes while pulling
```
