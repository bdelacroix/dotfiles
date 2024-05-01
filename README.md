## What it the purpose of this repo ?

The purpose of this repository is to allow quick and easy setup of the development environment I use on a daily basis. It gathers all my configuration files.

## Configuration files

### [Regolith](https://regolith-desktop.com/docs/using-regolith/install/)

```
ln -s ~/dotfiles/regolith3/Xresources ~/.config/regolith3/Xresources
ln -s ~/dotfiles/regolith3/i3/config ~/.config/regolith3/i3/config
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

```
sudo apt install zsh

sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
ln -s ~/dotfiles/.zshrc ~/.zshrc
```

Make ZSH default shell:

```
chsh -s $(which zsh)
```

Log out and log back then.

### Other Tools

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


## Fonts

- [Commit Mono](https://commitmono.com/) (used for OS purposes)
- [Dank Mono](https://philpl.gumroad.com/l/dank-mono) (used for VS Code coding font)

***Note :*** fonts for OS purpose are explicitely defined in `~/dotfiles/regolith3/Xresources` configuration file.
