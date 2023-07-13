# Ubuntu setup

1. [Introduction](#introduction)
2. [Git & Github](#git)
3. [Bash configuration](#bashconfig)
4. [Keyboard layout](#keyboard)
5. [KeePassXC](#keepassxc)
6. [Neovim](#nvim)
7. [Zathura](#zathura)
8. [(Optional) Alacritty](#alacritty)
9. [(Optional) Firefox](#firefox)
10. [Resources](#resources)

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

and replace your `.bashrc` in root with the one from the repo or just plain copy the contents there. Move also `.bash_aliases` to root and add any desired aliases, such as shortcuts to `cd` into certain directories. Notice that `vi` mode is enabled.



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

See my [nvim-config repo](https://github.com/vohonen/nvim-config).



<a name="zathura"></a>
## Zathura

See my [zathurarc repo](https://github.com/vohonen/zathurarc).



<a name="alacritty"></a>
## (Optional) Alacritty

See my [nvim-config repo](https://github.com/vohonen/nvim-config). 

Alacritty is surely optional as any other part of this config, but if one wants to use the full Neovim configuration but Alacritty and some Nerd Font are not installed, then one may consider reconfiguring nvimtree and potentially some other plugin as they rely on Nerd Font icons.



<a name="firefox"></a>
## (Optional) Firefox

Shortly something of my browser preferences. I would like to like [Brave](brave.com), but I have had issues with e.g. setting PPAs and some other stuff. Hence, I use Firefox for now. Install with 

```shell
sudo apt update && sudo apt install -y firefox
```

The more specific aspects of browser setup are with respect to the extensions. Pressing `ctrl+shift+a` one can manage add-ons, and I like to have first and foremost Vimium, Tomato Clock, AdBlocker Ultimate and Ecosia Search. After installing the add-ons, go to Firefox's add-ons page again by `ctrl+shift+a` and click the three dots after Vimium and choose Preferences. Then, at the bottom of the resulting Vimium Options page click the button "Show Advanced Options", and find the Default search engine field and change `google` -> `ecosia` in the default url (Ecosia utilises Bing search that is a little worse than Google's, but does the job adequately in a majority of the cases, and planting trees is more important).


<a name="resources"></a>
## Resources

Here's a list of some of the resources that were used for this configuration. The software-specific repos also got some links on installation etc. Additionally, Googling and Stack Overflow often do the trick.

[Git setup](https://git-scm.com/book/en/v2/Getting-Started-First-Time-Git-Setup)
[Generating a new SSH key](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)
[Connect to Github via SSH](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account)
[Ubuntu custom keyboard layouts](https://help.ubuntu.com/community/Custom%20keyboard%20layout%20definitions)

