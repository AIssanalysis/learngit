# Git learn  
## 1. install git  
- linux  
sudo apt-get install git  
- windows  
use this src:https://git-scm.com/downloads install git in windows, then right click menu find git bash  
- Mac OS  
Wait until me have a Mac book to study  
## 2. default setting  
```
$ git config --global user.name "Your Name"  
$ git config --global user.email "email@example.com"  
```
## 3. make a Git repository  
use this code change current directory become git repository  
```
$ git init  
```
## 4. Basic operation  
```
$ git add <file>  
add file in temporary area  
$ git commit -m<message>  
submit  
$ git status  
check git status  
$ git diff  
check git difference  
$ git log  
view log  
$ git reflog  
view reflog  
$ git reset --hard commit_id  
back version  
$ git checkout -- file  
drop modify in work area  
$ git reset HEAD <file>  
drop modify in temporary area
$ git rm  
as linux rm: delete file  
```
## 5. Github Remote repository  
if your pc have not set ssh, such add ssh  
```
$ ssh-keygen -t rsa -C "youremail@example.com"  
```
id_rsa is Private key  
id_rsa.pub is Public key  
set ssh in github.com fill id_rsa.pub in key  
### first create Remote repository  
```
$ git remote add origin git@github.com:yourgithubid/learngit.git  
link a remote repository  
$ git push -u origin master  
firse push modify  
$ git push origin master  
push modify  
```
### clone Remote repository  
```
$ git clone git@github.com:yourgithubid/repositoryname.git  
```
if only open http port, you can  
```
$ git clone https://github.com/yourgithubid/repositoryname.git  
```

### branch  

1. create  
```
$ git branch dev(branchname)  
$ git checkout dev  
```
  
The above two lines can be simplified to  
```
$ git checkout -b dev  
```
checkout -b mean create and switch, only checkout mean switch  

2. check  
```
$ git branch  
```

Current branch have * label  
you can work on new branch same as on master  

3. merge  
First of all, you should switch to the branch you need. such as:  
```
$ git checkout master  
$ git merge dev  
```
Conflict when two branches merge, you should Manually solved this problem  

4. delete  
```
$ git branch -d dev  
delete local branch  
$ git push origin --delete branchname  
delete remote branch
```
