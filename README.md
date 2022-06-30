## Ubuntu Personal Configuration

This repository was created to contain the necessary setup after new installation of Ubuntu OS.

__TOC__

### Install Tools from Terminal

* General Tools:

```bash
sudo apt install -y terminator gparted dconf-editor subversion git ssh meld picocom net-tools pinta hardinfo cutecom putty vim gimp mosquitto mosquitto-clients ubuntu-restricted-extras rar unrar p7zip-full p7zip-rar neofetch curl openssh-server mlocate filezilla grub-customizer
```

* Gnome Environment:

```bash
sudo apt install -y gnome-session gdm3 chrome-gnome-shell gnome-tweaks gnome-system-monitor gnome-shell-extensions
```

### User Permissions

* Add user to root group
```bash
xhost +si:localuser:root -> x
```
* Enable permissions on usb ports
```bash
sudo usermod -a -G dialout $(whoami)
sudo adduser $(whoami) dialout
```

