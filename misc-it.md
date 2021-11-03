# Miscellaneous IT instructions

## Configure ultan (our great computing node) for your computer:
- first you need ssh keys (although you probably have ones in `~/.ssh` folder)
- in case you don't [here's](https://upcloud.com/community/tutorials/use-ssh-keys-authentication/) simple intro how to manage ssh-keys
- add these lines to ~/.ssh/config
```
# Helsinki ultan
Host ultan
  ProxyJump <HELSINKI USER>@melkinkari.cs.helsinki.fi
  HostName ultan.it.helsinki.fi
  User <HELSINKI_USERNAME>
  UseKeychain yes
  IdentityFile <SSH KEY FILE>
```
- you will need to configure .ssh/authorized_keys files on both machines to have your local machines ssh keys (on mac you can copy the ssh keys to clipboard with pbcopy):

```
pbcopy < ~/.ssh/<SSH KEY FILE>
```
- add copied key to .ssh/authorized_keys on jump server (melkinkari):
```
ssh <HELSINKI USERNAME>@melkinkari.cs.helsinki.fi
pico .ssh/authorized_keys
```
- Cmd+[V] to add the key
- And then from melkinkari connect ultan and add keys from clipboard:
```
ssh <HELSINKI USERNAME>@ultan.it.helsinki.fi
pico .ssh/authorized_keys
```
- And same thing (Cmd+[V])
ps. if you’re username on the local computer is your `<HELSINKI USERNAME>` you can ignore it in `~/.ssh/config`
Now you have ultan ssh configured! You can test it with:
`ssh ultan`

## Remote access to Turso via VSCode
- [Developing on Remote Machines using SSH and Visual Studio Code](https://code.visualstudio.com/docs/remote/ssh)
- copy ssh key [copy-ssh-id](https://www.ssh.com/academy/ssh/copy-id)
- install Visual Studio Code Remote extension (https://code.visualstudio.com/docs/remote/ssh)
- add configuration to ~/.ssh/config
```
# Helsinki HPC
Host turso.cs.helsinki.fi
  HostName turso.cs.helsinki.fi
  User <HELSINKI_USERNAME>
  UseKeychain yes
  IdentityFile <SSH KEY FILE>
```
- log in to turso.cs.helsinki.fi & run:
```
module load nodejs
npm install minimist
```
- additionally create link to your home folder from project folder (not enough space in the home folders)
```
mkdir $PROJ/.vscode-server
ln -s $PROJ/.vscode-server ~
```
on VScode connect to turso.cs.helsinki.fi
(this is done via Cmd+Shift+P: Remote-SSH: Connect to Host…)

## Guide to use former Ukko file server
Simple solution to access data on `turso.cs.helsinki.fi`
​
1. install macFUSE
2. mount the server
3. profit!
​
Mac users:
[Download](https://github.com/osxfuse/osxfuse/releases/download/macfuse-4.1.0/macfuse-4.1.0.dmg) the macFUSE extension to your system and install. It asks you to give permission in system settings and restarts the system, please save remember to save your work before!
[Download](https://github.com/osxfuse/sshfs/releases/download/osxfuse-sshfs-2.5.0/sshfs-2.5.0.pkg) and install.
​
Run the following on terminal:
```zsh
ssh-keygen -o -a 100 -t ed25519 -f ~/.ssh/id_ed25519 -C "[YOUR EMAIL]@helsinki.fi"
ssh-copy-id -i ~/.ssh/id_ed25519 [HY_USERNAME]@turso.cs.helsinki.fi
sshfs [HY_USERNAME]@turso.cs.helsinki.fi:/wrk/group/hipercog/project_PSICAT/old-analyses/ ~/ukko -ovolname=ukko
```