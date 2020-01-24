
# Workflows with git-flow (demonstration)

By installing [git-flow](https://github.com/petervanderdoes/gitflow-avh/wiki/Installing-on-Linux,-Unix,-etc.), you'll have a handful of extra commands available. Each of these commands performs multiple tasks automatically and in a predefined order. And voila - there we have our workflows!

git-flow is by no means a replacement for Git. It's just a set of scripts that combine standard Git commands in a clever way.

Strictly speaking, you wouldn't even have to install anything to use the git-flow workflows: you could easily learn which workflow involves which individual tasks - and simply perform these Git commands (with the right parameters and in the right order) on your own. The git-flow scripts, however, save you from having to memorize all of this.



# Installation procedure

1. Install [git-flow](https://github.com/petervanderdoes/gitflow-avh/wiki/Installing-on-Linux,-Unix,-etc.).

```
sudo apt-get install git-flow
```

2. We can check if `git-flow` is successfully installed by:

```
dev@jino:~/git-demo$ git flow --version
usage: git flow <subcommand>

Available subcommands are:
   init      Initialize a new git repo with support for the branching model.
   feature   Manage your feature branches.
   bugfix    Manage your bugfix branches.
   release   Manage your release branches.
   hotfix    Manage your hotfix branches.
   support   Manage your support branches.
   version   Shows version information.
   config    Manage your git-flow configuration.
   log       Show log deviating from base branch.

Try 'git flow <subcommand> help' for details.
```

3. List the available commands:

```
dev@jino:~/git-demo$ git flow feature help
usage: git flow feature [list]
   or: git flow feature start
   or: git flow feature finish
   or: git flow feature publish
   or: git flow feature track
   or: git flow feature diff
   or: git flow feature rebase
   or: git flow feature checkout
   or: git flow feature pull
   or: git flow feature delete

    Manage your feature branches.

    For more specific help type the command followed by --help
```




## Initialization and creating feature branches

1.) Let's initialize it in a new project with `git flow init`

```
dev@jino:~/git-demo$ git flow init
Initialized empty Git repository in /home/dev/git-demo/.git/
No branches exist yet. Base branches must be created now.
Branch name for production releases: [master] 
Branch name for "next release" development: [develop] 

How to name your supporting branch prefixes?
Feature branches? [feature/] 
Bugfix branches? [bugfix/] 
Release branches? [release/] 
Hotfix branches? [hotfix/] 
Support branches? [support/] 
Version tag prefix? [] 
Hooks and filters directory? [/home/dev/git-demo/.git/hooks]
```

**Demo:** [git flow init](https://youtu.be/vgSfyibTK3c)


2.) git flow feature start [feature name]

```
dev@jino:~/git-demo$ git flow feature start login
Switched to a new branch 'feature/login'

Summary of actions:
- A new branch 'feature/login' was created, based on 'develop'
- You are now on branch 'feature/login'

Now, start committing on your feature. When done, use:

     git flow feature finish login

dev@jino:~/git-demo$ git branch
  develop
* feature/login
  master
```

**Demo:** [git flow feature start ](https://youtu.be/KVLlYyXE1ww)


3.) git flow feature finish [feature name]

```
dev@jino:~/git-demo$ git branch
  develop
* feature/login
  master
dev@jino:~/git-demo$ git flow feature finish login
Switched to branch 'develop'
Already up to date.
Deleted branch feature/login (was bf2f9c2).

Summary of actions:
- The feature branch 'feature/login' was merged into 'develop'
- Feature branch 'feature/login' has been locally deleted
- You are now on branch 'develop'

dev@jino:~/git-demo$ git branch
* develop
  master
```


**Demo:** [git flow feature finish](https://youtu.be/fmNMz-ImDT8)



## Managing release branches


1.) git flow release start [release version]


```
dev@jino:~/git-demo$ git branch
* develop
  master
dev@jino:~/git-demo$ git flow release start v1.0.0
Switched to a new branch 'release/v1.0.0'

Summary of actions:
- A new branch 'release/v1.0.0' was created, based on 'develop'
- You are now on branch 'release/v1.0.0'

Follow-up actions:
- Bump the version number now!
- Start committing last-minute fixes in preparing your release
- When done, run:

     git flow release finish 'v1.0.0'

dev@jino:~/git-demo$ git branch
  develop
  master
* release/v1.0.0
```

**Demo:** [git flow release start](https://youtu.be/lLWzDkeTeIYgif)


2.) git flow release finish [release version]


```
dev@jino:~/git-demo$ git branch
  develop
  master
* release/v1.0.0
dev@jino:~/git-demo$ git flow release finish v1.0.0
Switched to branch 'master'
Deleted branch release/v1.0.0 (was bf2f9c2).

Summary of actions:
- Release branch 'release/v1.0.0' has been merged into 'master'
- The release was tagged 'v1.0.0'
- Release branch 'release/v1.0.0' has been locally deleted
- You are now on branch 'master'

dev@jino:~/git-demo$ git branch
  develop
* master
dev@jino:~/git-demo$ git tag
  v1.0.0
```


**Demo:** [git flow release finish](https://youtu.be/pP6caa5yOLw)



3.) Done you can now push your changes to `remote master branch` and also `do not forget to push your newly created tags`.





## Quick fix from master branch using Hotfixes!


1.) git flow hotfix start [hotfix name]


```
dev@jino:~/git-demo$ git branch
  develop
* master
dev@jino:~/git-demo$ git flow hotfix start broken-link
Switched to a new branch 'hotfix/broken-link'

Summary of actions:
- A new branch 'hotfix/broken-link' was created, based on 'master'
- You are now on branch 'hotfix/broken-link'

Follow-up actions:
- Start committing your hot fixes
- Bump the version number now!
- When done, run:

     git flow hotfix finish 'broken-link'

dev@jino:~/git-demo$ git branch
  develop
* hotfix/broken-link
  master
```


**Demo:** [git flow hotfix start](https://youtu.be/oznDFJ_xsb8)



2.) git flow hotfix finish [hotfix name]


```
dev@jino:~/git-demo$ git branch
  develop
* hotfix/broken-link
  master
dev@jino:~/git-demo$ git flow hotfix finish broken-link
Switched to branch 'develop'
Deleted branch hotfix/broken-link (was bf2f9c2).

Summary of actions:
- Hotfix branch 'hotfix/broken-link' has been merged into 'master'
- The hotfix was tagged 'broken-link'
- Hotfix branch 'hotfix/broken-link' has been locally deleted
- You are now on branch 'develop'

dev@jino:~/git-demo$ git branch
* develop
  master
dev@jino:~/git-demo$ git tag
  broken-link
  v1.0.0
```


**Demo:** [git flow hotfix finish](https://youtu.be/4Q8Y-wRQLdA):


3.) Done!, you can now push your changes to `remote master branch` and also `do not forget to push your newly created tags`, you can set [git aliases](https://git-scm.com/book/en/v2/Git-Basics-Git-Aliases) for git flow shorter commands.


### Git Aliases

[gist example](https://gist.github.com/MrMovl/b8d3f390e3c43e911bff19f45b11e32c)

### External reference


[Git flow](https://www.git-tower.com/learn/git/ebook/en/command-line/advanced-topics/git-flow)
