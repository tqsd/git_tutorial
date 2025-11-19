# Git Tutorial

Git is an open source versioning software.

## How to use

When editing an existing project on your local machine, you need to clone it first

```bash
git clone git@github.com:USERNAME/REPO.git
cd REPO
```

The link can be coppied from git repository website.

### Core Loop

The core git usage loop is:
edit -> status -> add -> commit -> push

When you edit your git project the updated files are displayed with command
```bash
git status
```

To start tracking files you can add them individually:
```bash
git add file1.py
```

or all together
```bash
git add .
```
Then with the use of `git status` you can check which files are staged (added).

You can make use of `.gitignore` file to make sure some files are not tracked.
Generally you want to omit tracking the cache files and environment files. Usually you can just copy existing `.gitignore` template to the root of your project and the git will then avoid adding the
listed files to the repository.

An example of such `.gitignore` file is [`Python.gitignore`](https://github.com/github/gitignore/blob/main/Python.gitignore).

when you have staged (added) your desired files you can than commit the changes.
Commit creates a snapshot of the current state.

```bash
git commit -m "Short commit message"
```

And lastly you can push to the repository
```bash
git push origin <branch>
```

### Branches and merging

You almost never want to work directly on `master`/`main`/`trunk` branch. You will want to work on a feature branch. To create a branch:

```bash
git checkout master
git pull origin master # update first
git checkout -b new-branch-name
```

This activates creates and activates the new branch `new-branch-name`.
After making changes you then do

```bash
git add .
git commit -m "Implemented feature on new branch"
git push -u origin new-branch-name
```

the `-u` sets the upstream so that later you can just `git push`.

#### Merging

When you want to merge the codebase in two branches you can
do the following:
```bash
git checkout master  # swich back to the master branch
git pull origin master # Check if some updates were submitted to the master branch
git merge new-branch-name  # Merge the newely created branch into master
git push
```
The merging process will let you know if there are some conflicts. If there are they must be fixed manually. If not the merge process will automatically commit the changes.

If there is a merge conflict the `git merge` will let you know and the conflicts will be
marked like:
```bash
<<<<<<< HEAD
your version on current branch
=======
other branch’s version
>>>>>>> new-branch-name
```
You must manually remove the git marks and select which version you want to keep or rewrite it completely.

Then again you need to add, comit push

```bash
git add conflicted_file.py
git commit
# or
git merge --continue
```


## Installation

On Linux systems git is usually installed out of the box.

On Windows git must be installed [manually](https://git-scm.com/install/windows).

## SSH Key setup

In order to use git effectively (and securely) one needs to configure ssh keys.
This lets you use git through ssh protocol, where connection is authenticated for 
you automatically. Without it you must resort to https protocol, where for each
api call you must enter a password.

The idea is the following:
1. you create a public/private key pair on your machine,
2. then you submit the public key to github,
3. you give your agent access to the private key.

### Linux

On Linux systems to generate the key you do the following:
1. First check if you already have some keys
```bash
ls ~/.ssh
```
If you see something like

```bash
id_ed25519
id_ed25519.pub
```
then you already have the keys

2. If not, then you must generate the keys:
```bash
ssh-keygen -t ed25519 -C "your.email@example.com"
```
Then press enter to choose the default options and the keys will be generated for you.

3. Add SSH keys to your ssh agent

```bash
# Start the ssh-agent
eval "$(ssh-agent -s)"
# Add the new private key
ssh-add ~/.ssh/id_ed25519
```
4. Add the public key to github

```bash
cat ~/.ssh/id_ed25519.pub
```

Copy the whole line and add paste it to the github


Github -> Settings -> SSH and PGP keys -> New SSH key

### Windows
The process for windows is the same as  for linux, but inside of the gitbash

To enable the windows SSH Agent to persist when you work across VS Code or other programs
enable the agent $Win+R$, `services.msc`, OpenSSHE Authenitication Agent, properties, startup type -> Automatic
### MacOS
