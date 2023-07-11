# Ubuntu setup

1. [Introduction](#introduction)
2. [Git & Github](#git)
3. [Bash configuration](#bashconfig)
4. [Keyboard layout](#keyboard)
5. [KeePassXC](#keepassxc)
6. [Neovim](#nvim)
7. [Zathura](#zathura)
8. [(Optional) Alacritty](#alacritty)
9. [Resources](#resources)

<a name="introduction"></a>
## Introduction
This is my setup on Ubuntu (or more generally, Debian) machines. This document should guide one to easily configure new machines to match it. Keep in mind that superuser rights are required, and in some cases PPAs are used.  

Most of the sections refer to other repositories, so it is easier for me to maintain proper configuration files and installation instructions.



<a name="git"></a>
## Git & Github

It seems intuitive to start by configuring Git and connecting to Github via the command line. Some convenience aliases for `git`:

```shell
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.co checkout
git config --global alias.st status
```

Set also username and email with the same command but with arguments `user.name "username"` and `user.email example@email.com`.

Next, connect to Github via `ssh`. First, generate a new SSH key with using 

```shell
ssh-keygen -t ed25519 -C "example@email.com" 
```

remembering to change the email address to your Github email. The prompt asks to "Enter a file in which to save the key", and one can just press enter to accept default file location. Then, set a secure passphrase.

After generating a new key, it must be added to the ssh-agent. Start the agent and add the key with 

```shell
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```

Then, one can add the key to the desired Github account, see [Github instructions](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account) if unsure how to proceed with that.



<a name="bashconfig"></a>
## Bash configuration

Clone the repo with 

```shell
git clone git@github.com:vohonen/ubuntu-setup.git 
```

and replace your `.bashrc` in root with the one from the repo or just plain copy the contents there. Move also `.bash_aliases` to root and add any desired aliases, such as shortcuts to `cd` into certain directories. Finally, enable `vi` mode by running the command 

```shell
set -o vi
```



<a name="keyboard"></a>
## Keyboard layout

This part assumes that one uses a Finnish keyboard layout. Similar modifications can be done to any language keyboard layout. 

As per [Bash configuration](#bashconfig), clone the repo or copy the file contents of `fi` in the directory `/usr/share/X11/xkb/symbols`. Additionally, swap `esc` and `caps lock` by running the command 

```shell
dconf write /org/gnome/desktop/input-sources/xkb-options "['caps:swapescape']"
```


<a name="keepassxc"></a>
## KeePassXC

TBI


<a name="nvim"></a>
## Neovim

Sadly, at the moment the `nvim` is not maintained very attentively in `apt` and hence a PPA should be used if one does not want to install manually. Unfortunately, the stable PPA is also practically buried, so the [unstable PPA](https://launchpad.net/~neovim-ppa/+archive/ubuntu/unstable) must be used.

First, check that you can use `add-apt-repository` by installing the required package:

```shell
sudo apt-get update
sudo apt-get install software-properties-common
```

Then, the PPA can be added and Neovim installed from it with the required Python modules. 

```shell
sudo add-apt-repository ppa:neovim-ppa/stable
sudo apt-get update
sudo apt-get install neovim
sudo apt-get install python-dev python-pip python3-dev python3-pip
```

To set `nvim` as the default editor, run 

```shell
sudo update-alternatives --install /usr/bin/editor editor /usr/bin/nvim 60
sudo update-alternatives --config editor
```




<a name="zathura"></a>
## Zathura


<a name="alacritty"></a>
## (Optional) Alacritty


<a name="resources"></a>
## Resources

Here's a list of some of the resources that were used for this configuration. Additionally, Googling and Stack Overflow often do the trick.

[Git setup](https://git-scm.com/book/en/v2/Getting-Started-First-Time-Git-Setup)
[Generating a new SSH key](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)
[Connect to Github via SSH](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account)
[Ubuntu custom keyboard layouts](https://help.ubuntu.com/community/Custom%20keyboard%20layout%20definitions)
[Installing Neovim](https://github.com/neovim/neovim/wiki/Installing-Neovim)

