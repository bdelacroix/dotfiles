## What it the purpose of this repo ?

The purpose of this repository is to allow quick and easy setup of the development environment I use on a daily basis. It gathers all my configuration files.

## Common packages

```
sudo apt install curl vim
npm install --global yarn
```

## Configuration files

### [Regolith](https://regolith-desktop.com/docs/using-regolith/install/)

```
ln -s ~/dotfiles/regolith3/Xresources ~/.config/regolith3/Xresources
ln -s ~/dotfiles/regolith3/i3/config ~/.config/regolith3/i3/config
```

Install `i3xrocks` packages:

```
sudo apt install i3xrocks-wifi i3xrocks-focused-window-name i3xrocks-volume i3xrocks-battery
```

```
regolith-look refresh
```

### [Tmux](https://github.com/tmux/tmux)

```
ln -s ~/dotfiles/tmux/.tmux.conf ~/.tmux.conf
```

`tmux` requires the installation of [TPM](https://github.com/tmux-plugins/tpm), a plugin used to managed `tmux` dependencies:

```
git clone https://github.com/tmux-plugins/tpm ~/.tmux/plugins/tpm

# Install TPM plugins defined in .tmux.conf
~/.tmux/plugins/tpm/bin/install_plugins
```

### [Spotify](https://www.spotify.com)

#### Installation

Follow the given installation process [here](https://www.spotify.com/us/download/linux/).

Then:
```
sudo chmod a+wr /usr/share/spotify
sudo chmod a+wr /usr/share/spotify/Apps -R
```

#### Theming

[Spicetify](https://spicetify.app) is a powerful tool to easily theme and extend the Spotify client.

Follow the [installation guide](https://spicetify.app/docs/advanced-usage/installation/#linux-and-macos) to install `Spicetify`:

```
curl -fsSL https://raw.githubusercontent.com/spicetify/spicetify-cli/master/install.sh | sh
```

Reload terminal then:

```
spicetify backup apply enable-devtools
spicetify update
```

I am using the `Dribbblish` theme with `catppuccin-latte` color scheme. Please note installation process might differ with other themes.

```
git clone --depth=1 https://github.com/spicetify/spicetify-themes.git 

cd spicetify-themes
cp -r * ~/.config/spicetify/Themes

cd ~/.config/spicetify/Themes/Dribbblish
spicetify config current_theme Dribbblish color_scheme catppuccin-latte
spicetify config inject_css 1 replace_colors 1 overwrite_assets 1 inject_theme_js 1
spicetify apply

rm ~/.config/spicetify/Themes/Dribbblish/*.png
```

See more : https://spicetify.app/docs/advanced-usage/themes

### [Bat](https://github.com/sharkdp/bat)

```
sudo apt install bat
```

Due to a conflit with "bat" with another package, create a symlink "batcat > bat" to prevent issues with other packages/distributions

```
mkdir -p ~/.local/bin
ln -s /usr/bin/batcat ~/.local/bin/bat
```

Install Catppuccin Latte theme :

```
ln -s ~/dotfiles/bat  ~/.config/bat
bat cache --build
```

### [ZSH](https://github.com/ohmyzsh/ohmyzsh/wiki/Installing-ZSH)


Install ZSH:

```
sudo apt install zsh
ln -s ~/dotfiles/.zshrc ~/.zshrc
```

Install Oh My Zsh and used plugins:

```
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
```

Make ZSH default shell:

```
chsh -s $(which zsh)
```

Log out and log back then.

### Other Tools

Some tools that do not require dotfiles configuration, but are prerequired for my daily basis:

#### [Github CLI](https://github.com/cli/cli?tab=readme-ov-file)

Download package :

```
(type -p wget >/dev/null || (sudo apt update && sudo apt-get install wget -y)) \
	&& sudo mkdir -p -m 755 /etc/apt/keyrings \
        && out=$(mktemp) && wget -nv -O$out https://cli.github.com/packages/githubcli-archive-keyring.gpg \
        && cat $out | sudo tee /etc/apt/keyrings/githubcli-archive-keyring.gpg > /dev/null \
	&& sudo chmod go+r /etc/apt/keyrings/githubcli-archive-keyring.gpg \
	&& echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/githubcli-archive-keyring.gpg] https://cli.github.com/packages stable main" | sudo tee /etc/apt/sources.list.d/github-cli.list > /dev/null \
	&& sudo apt update \
	&& sudo apt install gh -y
```

Install :

```
sudo apt update
sudo apt install gh
```

Generate a [personal access token](https://github.com/settings/tokens) on Github :

```
git config --global credential.helper store
```

Do a `pull`/`push` command, and fill username and generated PEAP. Github should not ask credentials anymore!  

#### [VS Code](https://code.visualstudio.com/download#)

Settings are auto-synced in VS Code.

#### [Slack](https://slack.com/intl/fr-fr/help/articles/212924728-T%C3%A9l%C3%A9charger-Slack-pour-Linux--version-b%C3%AAta-)

```
sudo snap install slack
```

#### [Docker](https://docs.docker.com/engine/install/ubuntu/)

```
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update

# Install the latest version:
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

# Verify docker has been successfully installed
sudo docker run hello-world
```

Run Docker as a non root user (requires to log out):

```
sudo groupadd docker
sudo usermod -aG docker $USER
```

### [NVM](https://github.com/nvm-sh/nvm)

`nvm` (Node Version Manager) allows to quickly install and use different versions of node via the command line. 

```
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.2/install.sh | bash
```

### [Deno](https://docs.deno.com/runtime/getting_started/installation/)

`Deno` is a JavaScript and TypeScript runtime that was designed and built to be an alternative to Node.js

```
curl -fsSL https://deno.land/install.sh | sh
```

### [Phpactor](https://phpactor.readthedocs.io/en/master/usage/standalone.html)

`Phpactor` is a the main LSP for PHP support.

```
sudo apt install php

curl -Lo phpactor.phar https://github.com/phpactor/phpactor/releases/latest/download/phpactor.phar
chmod a+x phpactor.phar
mv phpactor.phar ~/.local/bin/phpactor
```

I am using VS code [extension](https://marketplace.visualstudio.com/items?itemName=phpactor.vscode-phpactor) for IDE completion.

#### [FZF](https://github.com/junegunn/fzf)

```
sudo apt install fzf
```

#### [Ripgrep](https://github.com/BurntSushi/ripgrep)

```
curl -LO https://github.com/BurntSushi/ripgrep/releases/download/13.0.0/ripgrep_13.0.0_amd64.deb
sudo dpkg -i ripgrep_13.0.0_amd64.deb
```


#### [Taskbook](https://github.com/klaudiosinani/taskbook)

```
sudo npm install --global taskbook
```

#### [Teams](https://snapcraft.io/teams-for-linux)

```
sudo snap install teams-for-linux
```

#### Redshift

Redshift is an open-source for managing screen luminosity.

```
sudo apt install redshift
```

> Please note symlinks provoques an unexpected error, place the configuration file in `~/.config/redshift.conf`


## Fonts

- [Commit Mono](https://commitmono.com/) (used for OS purposes)
- [Dank Mono](https://philpl.gumroad.com/l/dank-mono) (used for VS Code coding font)

***Note :*** fonts for OS purpose are explicitely defined in `~/dotfiles/regolith3/Xresources` configuration file.

If you want to apply your system font to Firefox, copy your installed font to `/usr/share/fonts`:

```
sudo cp ~/.local/share/fonts/CommitMono-400-Regular.otf /usr/share/fonts
```

## Keyboad layout

I am using [QWERTY-fr](https://github.com/qwerty-fr/qwerty-fr) keyboard layout for my daily usages.
