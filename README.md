# Ubuntu Personal Configuration

This repository was created to contain the necessary setup after new installation of Ubuntu OS.

## Tools

### Installed Tools

* General & Gnome Tools:

```bash
sudo apt install -y terminator gparted dconf-editor subversion git ssh sshpass meld picocom net-tools pinta hardinfo cutecom putty vim gimp mosquitto mosquitto-clients ubuntu-restricted-extras rar unrar p7zip-full p7zip-rar neofetch curl openssh-server mlocate filezilla tree fuse libfuse2 freecad librecad pulseaudio pavucontrol python3 python3-venv python3-pip &&\
sudo apt install -y gnome-control-center gnome-session gdm3 chrome-gnome-shell gnome-tweaks gnome-system-monitor gnome-shell-extensions xdg-desktop-portal-gnome gnome-screenshot
```

### Snap Tools

Run in terminal:

```bash
sudo snap install sublime-text --classic &&\
sudo snap install code --classic &&\
sudo snap install mqtt-explorer &&\
sudo snap install vlc &&\
sudo snap install arduino &&\
sudo snap install spotify &&\
sudo snap install postman &&\
sudo snap install termius-app &&\
sudo snap install kdenlive &&\
sudo snap install android-studio --classic &&\
sudo snap install wps-2019-snap &&\
sudo snap install onlyoffice-desktopeditors &&\
sudo snap install mqttx &&\
sudo snap install rpi-imager &&\
sudo snap install node-red
```


### Other Tools

- [x] [Chrome](https://www.google.com/intl/pt-PT/chrome/)
- [x] [Balenaetcher](https://www.balena.io/etcher/)
- [x] [Eagle](https://www.autodesk.com/products/eagle/free-download)
- [ ] VirtualBox
- [ ] Autenticação GOV
- [ ] Boot Repair
- [ ] Anydesk
- [ ] TeamViewer
- [ ] VNC 
- [ ] Wireshark
- [x] [4K video downloader](https://www.4kdownload.com/products/videodownloader/15)
- [x] [Rambox](https://rambox.app/download)
- [ ] Cura
- [x] [Kicad](https://www.kicad.org/download/ubuntu/)
- [x] [Draw.io](https://github.com/jgraph/drawio-desktop/releases/tag/v19.0.3)
- [ ] Sketchup for Web
- [ ] Sweet Home 3D
- [ ] Angry IP Scanner
- [ ] LFTP
- [x] [FortiClient VPN](https://www.fortinet.com/support/product-downloads)
- [x] [Grub Customizer](https://ubuntuhandbook.org/index.php/2022/04/install-grub-customizer-ubuntu-2204/)

## Applications Shortcuts

This procedure enable the shortcut to **AppImager** applications.
See `shortcuts` folder on this repository.

* Create a file with `.desktop` extension (`name.desktop`) in `/home/$(whoami)/.local/share/applications` path.

File contents:

```bash
#!/usr/bin/env xdg-open

[Desktop Entry]
Version=1.0
Type=Application
Terminal=false
Exec=[PATH_TO_EXECUTE]
Name=[NAME]
Comment=
Icon=[PATH_TO_ICON]
```
* Add permissions to file:

```bash
chmod +x name.desktop
```


## Gnome Extensions

- [x] [Caffeine](https://extensions.gnome.org/extension/517/caffeine/)
- [x] [Clipboard Indicator](https://extensions.gnome.org/extension/779/clipboard-indicator/)
- [x] [OpenWeather](https://extensions.gnome.org/extension/750/openweather/)
- [x] [Refresh Wifi Connections](https://extensions.gnome.org/extension/905/refresh-wifi-connections/)
- [x] [Disconnect Wifi](https://extensions.gnome.org/extension/904/disconnect-wifi/)
- [x] [Docker](https://extensions.gnome.org/extension/5103/docker/)
- [x] [Removable Drive Menu](https://extensions.gnome.org/extension/7/removable-drive-menu/)
- [x] [Sound input & output device chooser](https://extensions.gnome.org/extension/906/sound-output-device-chooser/)
- [x] [Status Area Horizontal Spacing](https://extensions.gnome.org/extension/355/status-area-horizontal-spacing/)
- [x] [NoAnnoyance v2](https://extensions.gnome.org/extension/2182/noannoyance/)
- [x] [Screenshot Tool](https://extensions.gnome.org/extension/1112/screenshot-tool/)
- [x] [Tweaks & Extensions in System Menu](https://extensions.gnome.org/extension/1653/tweaks-in-system-menu/)
- [x] [Places status indicator](https://extensions.gnome.org/extension/8/places-status-indicator/)
- [x] [Bring Out Submenu Of Power Off/Logout Button](https://extensions.gnome.org/extension/2917/bring-out-submenu-of-power-offlogout-button/)


## VS Code

### Open in Code menu

Run in terminal:

```bash
wget -qO- https://raw.githubusercontent.com/cra0zy/code-nautilus/master/install.sh | bash
```


### VS Code Extensions

- [ ] ms-vscode.cpptools
- [ ] shd101wyy.markdown-preview-enhanced
- [ ] platformio.platformio-ide
- [ ] ms-python.python
- [ ] espressif.esp-idf-extension
- [ ] fabiospampinato.vscode-diff
- [ ] funkyremi.vscode-google-translate
- [ ] ms-vscode-remote.remote-ssh
- [ ] yzhang.markdown-all-in-one
- [ ] xaver.clang-format
- [ ] ms-iot.vscode-ros
- [ ] ms-azuretools.vscode-docker
- [ ] eamodio.gitlens
- [ ] ms-vsliveshare.vsliveshare
- [ ] hediet.vscode-drawio
- [ ] streetsidesoftware.code-spell-checker
- [ ] GitLab.gitlab-workflow
- [ ] James-Yu.latex-workshop
- [ ] ms-vscode.live-server
- [ ] ms-vsliveshare.vsliveshare
- [ ] yzane.markdown-pdf

## Configuration

### User Permissions

* Add user to root group
```bash
xhost +si:localuser:root
```
* Enable permissions on usb ports
```bash
sudo usermod -a -G dialout $(whoami) &&\
sudo adduser $(whoami) dialout
```


### Bash RC File 

Open File:
```bash
code ~/.bashrc
```

Add in the end of the file the follow contents:
```bash
# get current branch in git repo
function parse_git_branch() {
	BRANCH=`git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/\1/'`
	if [ ! "${BRANCH}" == "" ]
	then
		STAT=`parse_git_dirty`
		echo "[${BRANCH}${STAT}]"
	else
		echo ""
	fi
}

# get current status of git repo
function parse_git_dirty {
	status=`git status 2>&1 | tee`
	dirty=`echo -n "${status}" 2> /dev/null | grep "modified:" &> /dev/null; echo "$?"`
	untracked=`echo -n "${status}" 2> /dev/null | grep "Untracked files" &> /dev/null; echo "$?"`
	ahead=`echo -n "${status}" 2> /dev/null | grep "Your branch is ahead of" &> /dev/null; echo "$?"`
	newfile=`echo -n "${status}" 2> /dev/null | grep "new file:" &> /dev/null; echo "$?"`
	renamed=`echo -n "${status}" 2> /dev/null | grep "renamed:" &> /dev/null; echo "$?"`
	deleted=`echo -n "${status}" 2> /dev/null | grep "deleted:" &> /dev/null; echo "$?"`
	bits=''
	if [ "${renamed}" == "0" ]; then
		bits=">${bits}"
	fi
	if [ "${ahead}" == "0" ]; then
		bits="*${bits}"
	fi
	if [ "${newfile}" == "0" ]; then
		bits="+${bits}"
	fi
	if [ "${untracked}" == "0" ]; then
		bits="?${bits}"
	fi
	if [ "${deleted}" == "0" ]; then
		bits="x${bits}"
	fi
	if [ "${dirty}" == "0" ]; then
		bits="!${bits}"
	fi
	if [ ! "${bits}" == "" ]; then
		echo " ${bits}"
	else
		echo ""
	fi
}

export PS1="\[\e[37m\]tiagofmmacedo\[\e[m\]\[\e[37m\]:\[\e[m\]\[\e[0;34m\]\W\[\e[m\]\[\e[0;34m\]\\$\[\e[m\]\[\e[34m\]\`parse_git_branch\`\[\e[m\] " 
```

Reload File:
```bash
source ~/.bashrc
```

### STM32 

If Error: `libusb_open() failed with LIBUSB_ERROR_ACCESS`
Run:
```bash
curl -fsSL https://raw.githubusercontent.com/platformio/platformio-core/master/scripts/99-platformio-udev.rules | sudo tee /etc/udev/rules.d/99-platformio-udev.rules && sudo service udev restart
```
Unplug and reconnect the board

## GIT

* Generate ssh keys:
```bash
ssh-keygen -t rsa -b 4096
```
```bash
ssh-keygen -t ed25519 -C "tiago.macedo@ceiia.com"
```

* Configure git:
```bash
git config --global user.name "Tiago Macedo" &&\
git config --global user.email tiago.macedo@ceiia.com
```

* Edit `.gitconfig` file:
```bash
code ~/.gitconfig
```

* Paste the follow contest:
```bash
[user]
	name = Tiago Macedo
	email = tiago.macedo@ceiia.com
# --------------- D I F F ---------------
[diff]
	tool = meld
[difftool]
	prompt = false
[difftool "meld"]
	cmd = meld "$LOCAL" "$REMOTE"
 
# --------------- M E R G E ---------------
[merge]
	tool = meld
[mergetool "meld"]
	cmd = meld "$LOCAL" "$MERGED" "$REMOTE" --output "$MERGED"
 
# --------------- A L I A S ---------------
[alias]
	co = checkout 
	cm = commit -m 
	st = status
	cl = clean -df
	pl = pull
	ps = push
```

## Disk Partition Size

```
/dev/sda1   ntfs            Recuperação     530MB
/dev/sda2   fat32           /boot/efi       100MB
/dev/sda3   ms reserved                      16MB
/dev/sda4   ntfs            Windows10       160GB
/dev/sda5   ext4            /                30GB
/dev/sda6   ext4            /home            50GB
/dev/sda7   linux-swap                        6GB
```
