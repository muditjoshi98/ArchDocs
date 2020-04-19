# Softwares and their Stuff...

## [bspwm & sxhkd](https://github.com/baskerville)
* Use external `rules` and `colors.sh` file for better window handling and coloring in bspwm.
* sxhkd stucks on repeated config reload.
* If auto-starting anything via bspwm (especially sxhkd) remember to kill it's previous instance first cause on bspwm restart an new instance of that program will start which reduce performance.

## Disk Management

* For disk analysis `duc`
* `udisk2`, `udiskie` and `ntfs-3g` for external device mounting.
* For more details refer to [cleanArch.md](cleanArch.md)

## Firefox

* userChrome theme used : https://github.com/eduardhojbota/moonlight-userChrome
* add user chrome in profile.
* tabliss

## Fonts
* Noto-Fonts and Noto-Font-Emoji
* Hack Nerd Patched Font
* JetBrains Mono
* Font Awesome (If needed)

## Gestures
* Install `libinput-gestures` AUR package.
* Basic commands : `libinput-gestures-setup (autostart/autostop/start/stop/status/restart)`
* Store your config fiel in `$HOME/.config/libinput-gestures.conf`

## [Mirrors](https://wiki.archlinux.org/index.php/Mirrors)
* Install `pacman-contrib` package.
* Generated list from https://www.archlinux.org/mirrorlist/
* Run `rankmirrors -n *no of mirrors*` command on list to generate n fastest servers.
* Replace it with default mirror list `/etc/pacman.d/mirrorlist`

## [Node JS](https://github.com/polybar/polybar)

### nvm(Node Version Manager)
A node js installer for installing multiple version of node js simultaneoulsy.

```
# Set up Node Version Manager
source /usr/share/nvm/init-nvm.sh

# Install Latest version
nvm install node

# To install specific version
nvm install 'version' 

# To list available versions
nvm (ls-remote/ls) 

#To use specific version in shell
nvm use (node/'version') 
```

## [Polybar](https://github.com/polybar/polybar)
* External script
    * `bluetoothctl.sh`
    * `spotify.py`
* Don't forget to scale Noto Emoji otherwise it will shown very big.
* Prefered to use Xresources colors whereever possible.


## [Ranger](https://github.com/ranger/ranger)
* Devicon Plugin for icons.
* ranger-git package for ueberzug support for image preview in `st`
* use mpv to open gifs as feh cannot play it in `rifle.conf`
* Enable previews for pdf, image and videos in `scope.sh`

## [Rofi](https://github.com/davatorium/rofi)
* Use 2 files `colors.rasi` and `config.rasi` and source `colors.rasi` in `config.rasi`
* Use `/* vim:ft=css` for syntax-highlighting.
* Used dmenu type look.

## [st and slock](https://suckless.org/)

* ### st Patches

    * Bold is not bright
    * BoxDraw
    * CopyURL
    * Font2
    * Invert

* Use libxft-bgra AUR version for emoji support in terminal
* Create separate color.h files for easy colorscheme change and add it in config.h

## [Vim](https://wiki.archlinux.org/index.php/Vim)

* Theme : Purify (https://github.com/kyoz/purify/)

### NeoVim
Config file `$HOME/.config/nvim/init.vim`

Autoload `$HOME/.local/share/nvim/site/autoload`

### [Vim-Plug](https://github.com/junegunn/vim-plug)

Minimalist Vim Plugin Manager

Install :
```
# Vim (~/.vim/autoload) & Neovim (~/.local/share/nvim/site/autoload)
curl -L -o 'output_file' https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
```
init.vim :
```
" Plugins will be downloaded under the specified directory.
call plug#begin('~/.vim/plugged')

" Declare the list of plugins.
Plug 'tpope/vim-sensible'
Plug 'junegunn/seoul256.vim'

" List ends here. Plugins become visible to Vim after this call.
call plug#end()
```
* Restart vim or source  conf file.
* `:PlugInstall` to install plugins
* `:PlugUpdate` to update plugins
* TO remove a plugin remove it from config file, then restart Vim and then run`:PlugClean` to remove it.

### Vim Plugins

* vim-airline/vim-airline
* ctrlpvim/ctrlp.vim (https://ctrlpvim.github.io/ctrlp.vim/)
* ryanoasis/vim-devicons
* christoomey/vim-tmux-navigator (https://github.com/christoomey/vim-tmux-navigator)
* airblade/vim-gitgutter
* preservim/nerdcommentor
* preservim/nerdtree

## xAutoLock
* Autostart in `.xinit`
* `xautolock -time 5 -locker "slock & sleep 2 && xset dpms force off" -corners +-00 -cornerdelay 3 -cornerredelay 120 -detectsleep &`
* Need to implement auto suspend after some time.
* Enable `lock.service` file to lock on suspend.

## [Zathura](https://pwmt.org/projects/zathura/)
* Install `zathura` along with required dependency like `zathura-pdf-poppler` for pdf support.
* Edit `zathura_setting`, `colors.sh` and run `zathura-colors.sh` to gen `zathurarc`

## Other small programs and things ...
* [picom](https://github.com/yshui/picom) - Compositor for X11
* Used [pywal](https://github.com/dylanaraps/pywal/) to generate basic color files and change color scheme accoring to requirement.
* `PS4='+$BASH_SOURCE> ' BASH_XTRACEFD=7 bash -xl 7> file_name` to dry run bash initialization to check where which variable is intialized.
* `feh` as image viewer and wallpaper setter.
* `bash-completion` package for command completion in bash
* For emoji support in urxvt use `rxvt-unicode-wcwidthcallback` AUR package.
* Guvcview for webcam.
* [TLP](https://wiki.archlinux.org/index.php/TLP) for advance power management (or simly save laptop battery)
* tmux
* [Microcode](https://wiki.archlinux.org/index.php/Microcode)
* An NTP tool like [chrony](https://wiki.archlinux.org/index.php/Chrony)
* Pulsemixer
* `ytop` and `htop` for system monitoring.
* `xmodmap` and `xev` to check for keycodes.
* `maim` for screenshot tool
