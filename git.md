# Git Tutorial

Git is an open source versioning software.

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
