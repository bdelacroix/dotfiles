## What it the purpose of this repo ?

The purpose of this repository is to allow quick and easy setup of the development environment I use on a daily basis. It gathers all my configuration files.

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

### [Spotify](https://www.spotify.com/us/download/linux/)

#### Installation

```
curl -sS https://download.spotify.com/debian/pubkey_6224F9941A8AA6D1.gpg | sudo gpg --dearmor --yes -o /etc/apt/trusted.gpg.d/spotify.gpg
echo "deb http://repository.spotify.com stable non-free" | sudo tee /etc/apt/sources.list.d/spotify.list
sudo apt-get update && sudo apt-get install spotify-client

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
git clone https://github.com/zsh-users/zsh-autosuggestions.git $ZSH_CUSTOM/plugins/zsh-autosuggestions
```

Make ZSH default shell:

```
chsh -s $(which zsh)
```

Log out and log back then.

### Other Tools

Some tools that do not require dotfiles configuration, but are prerequired for my daily basis:

#### [Docker](https://docs.docker.com/engine/install/ubuntu/)

```
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl
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
