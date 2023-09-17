# Creating ssh key for authentication and commit signing


### generate ssh key pair

windows open git bash from terminal, you cant use cmd or powershell for this step. Linux, Macos users can be done in any terminal

```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```

select path where you want to save your key pair. convinient way .ssh directory in your home folder

```bash
> Enter a file in which to save the key (/c/Users/YOU/.ssh/id_ALGORITHM):[Press enter]

~/.ssh/id_ed25519
```

it will ask enter passphrese, basically skip with enter
```bash
> Enter passphrase (empty for no passphrase): [Type a passphrase]
> Enter same passphrase again: [Type passphrase again]
```
### starting ssh-agent

note: windows users must be done this step on git-bash 
```bash
eval "$(ssh-agent -s)"

#> Agent pid 59566
```

add your ssh key to your ssh agent, again windows users must be use git-bash terminal

```bash
ssh-add ~/.ssh/id_ed25519
```

## Authentication on github with ssh


```bash
cat ~/.ssh/id_ed25519.pub
```
if this step not work for windows users go to `%userprofile%/.ssh/id_ed25519.pub` file and copy key manually
- open a browser, and go [ssh and gpg keys](https://github.com/settings/keys) on github settings

- click add new ssh, select key type autorization key and paste your public key then save

validate your ssh key 
windows users must be use gitbash for this
```bash
ssh -T git@github.com
> "Hi YourUserName! You've successfully authenticated, but GitHub does not provide shell access."
```


## using your ssh as commit signature key

### set git to sign commits with ssh
tell git to use commit signature key
```bash
git config --global commit.gpgsign true
```
tell git about your key type
```bash
git config --global gpg.format ssh
```
if ssh agent doesnt run, spin it up
#note for windows user this step must be on git-bash
```bash
eval "$(ssh-agent)"
```
tell git your private key

```bash
# note you can use same key for auth & sign 
# if you created a key before for auth atc, you can use same key
git config --global user.signingkey ~/.ssh/id_ed25519
```



Use the -S flag when signing your commits:
```bash
git commit -S -m "My commit msg"
```

optional if you dont want to use -S flag, set git to sign commits by default

```bash
git config --global commit.gpgsign true
```
### telling git your signing key
copy your public key
```bash
cat ~/.ssh/id_ed25519.pub
```
if this step not work for windows users go to `%userprofile%/.ssh/id_ed25519.pub` file and copy key manually
- open a browser, and go [ssh and gpg keys](https://github.com/settings/keys) on github settings

- click add new ssh, select key type signing key and paste your public key then save
