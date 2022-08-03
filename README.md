# Fedora-Settings

Things to do after installing Fedora 36

## Enable tap to click

I don't understand why this isn't enabled by default, but at least you should only have to do this once. Open settings, go to Mouse & Touchpad and enable tap to click.

## Update DNF settings

DNF is an excellent package manager but it can benefit from a few tweaks. This will take a while the first time it runs, but then it should be much faster and it will default to Y rather than N at each yes or no prompt (just like APT).


`sudo nano /etc/dnf/dnf.conf`

Add the following (you can use Shift Ctrl V to paste into the Terminal):

```
fastestmirror=True
max_parallel_downloads=10
defaultyes=True
keepcache=True
```
Ctrl x to save

`sudo dnf clean all`

`sudo dnf update`

## Enable RPM Fusion

https://rpmfusion.org

Enables the RPM Fusion repositories and installs a bunch codecs
```
sudo dnf install https://mirrors.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm https://mirrors.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm

sudo dnf groupupdate core

sudo dnf groupupdate multimedia --setop="install_weak_deps=False" --exclude=PackageKit-gstreamer-plugin

sudo dnf groupupdate sound-and-video
```

## Install POP Shell

The Pop!_OS tiling shell extension is awesome, after installing you will need to log out and back in and then enable it in your Extensions, it will appear as a built in extension.

`sudo dnf install gnome-shell-extension-pop-shell xprop`

## Enable Flatpak

One day all software will be installed this way, this enables Flatpak and applies a fix to make installed apps match your locally installed theme.

```
flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo
  sudo flatpak override --filesystem=$HOME/.themes
sudo flatpak override --env=GTK_THEME=my-theme
```

## Install Fish
The Friendly Interactive Shell is definitely my preferred way to use the terminal, this will install it and set it as the default shell for your user.

https://fishshell.com/

```
sudo dnf install util-linux-user
sudo dnf install fish
chsh -s /usr/bin/fish
```
## Change hostname
Choose a meaningful name so not every device on your network is called Fedora

`sudo hostnamectl set-hostname FedoraMyPC`

## Install software
Just a few utilities I find useful and install as a matter of course.
```
sudo dnf install htop
sudo dnf install neofetch
sudo dnf install bpytop
sudo dnf install gnome-tweaks
```

## Customisation

Use Tweaks to enable the Maximize and Minimize controls on your windows and add the weekday to the clock.

## Gnome Extensions

These are a few of my favourite must have Gnome extensions:

### Bluetooth Quick Connect

https://extensions.gnome.org/extension/1401/bluetooth-quick-connect/

Puts additional features into the Bluetooth menu, essential for bluetooth keyboard and mouse users.

### Frippery Move Clock

https://extensions.gnome.org/extension/2/move-clock/

Really simple extension that puts the clock on the right hand side of the panel - where it should be.

### Light Dark Theme Switcher

https://extensions.gnome.org/extension/4968/lightdark-theme-switcher/

Does what it says, adds an icon to the panel to switch between light and dark themes.

