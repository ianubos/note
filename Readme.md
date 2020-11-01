# How to use Github

## Git & GitHub Resources
[Markdown language cheetsheet](https://guides.github.com/pdfs/markdown-cheatsheet-online.pdf)
[Git branches explanation](https://git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging)

## Brad Traversy's Guide of Git & GitHub
[youtube link](https://www.youtube.com/watch?v=SWYqp7iY_Tc)
commands
```
git init
git config --global user.name 'Brad Traversy'
git config --global user.email 'me@bradtraversy.com'
git add index.html
git status
git rm --cached index.html    //remove
git add *.html    // all the html file
git add .   //all the files
git commit    //vim editor be opened 
git commit -m 'Changed app.jus'
touch .gitignore     //Just write filename and prevent the file to go to staging area.
```
.gitignore
```
log.txt
/dir2
```
commands
```
git branch login
git chechout login    // Switch the branch
touch login.html
git add .
git commit -m "login form"
git chechout master
# The login.html file is gone, because you are in master branch, not in login branch!
git merge login
git remote add orign https://github.com/bradtraversy/myappsample.git
git remote   // See the remote repos
git push -u origin master
touch README.md
git add .
git commit -m "Added readme"
git push

git pull  //up-to-date


git branch -d <branch name> //delete a branch
```






# Problems
## .git file does not show up in VSCode
.git file is not showed in the vscode explorer. To solve this problem,
1. vscode menu -> Preference -> Setting
2. Search "files.exclude" which decides what types of files do not show.
3. Delete /.git
![setting of vscode](/images/image.png)

## Cannot make by "git branch login"
That is because git's master branch has not been made yet until you firstly commit your repo.
What you need to do is first commit! -> [stackoverflow's answer](https://stackoverflow.com/questions/9162271/fatal-not-a-valid-object-name-master/9162347)

## Non-related repos' merge method
```
fatal: refusing to merge unrelated histories
```
That would be happened when you try to merge unrelated repositories.
Use the option --allow-unrelated repositories.
```
git pull origin master --allow-unrelated-histories
```

[Solution url](https://www.educative.io/edpresso/the-fatal-refusing-to-merge-unrelated-histories-git-error)






