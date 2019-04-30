### Create a remote repository and push
```git
git init
git add .
git commit -am 'init'

git config --local user.name username
git config --local user.email email

git config --list   //check config

git config --local core.ignorecase false // turn case sensitivity off

// use http to connect
curl -u username https://api.github.com/user/repos -d '{"name":"RepoName"}'

// update
git remote add origin git@github.com:username/RepoName.git 

git push origin master
```