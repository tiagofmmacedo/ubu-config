## Ubuntu Personal Configuration

This repository was created to contain the necessary setup after new installation of Ubuntu OS.

### Install Tools from Terminal

* General Tools:

```bash
sudo apt install -y terminator gparted dconf-editor subversion git ssh meld picocom net-tools pinta hardinfo cutecom putty vim gimp mosquitto mosquitto-clients ubuntu-restricted-extras rar unrar p7zip-full p7zip-rar neofetch curl openssh-server mlocate filezilla grub-customizer
```

* Gnome Tools:

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

### Applications Shortcuts

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

- [ ] Chrome
- [ ] Balenaetcher
- [ ] Eagle
- [ ] VirtualBox
- [ ] Autenticação GOV
- [ ] Boot Repair
- [ ] Anydesk
- [ ] TeamViewer
- [ ] VNC 
- [ ] Wireshark
- [ ] 4K video downloader
- [ ] 4K youtube to mp3
- [ ] Freecad
- [ ] Rambox
- [ ] Cura
- [ ] Kicad
- [ ] Sketchup for Web
- [ ] Sweet Home 3D
- [ ] Angry IP Scanner
- [ ] LFTP



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


### Gnome Extensions

- [ ] Caffeine 
- [ ] Center Area Horizontal Spacing 
- [ ] Clipboard Indicator
- [ ] CPU Power Manager
- [ ] Dash to Dock
- [ ] Desktop icons
- [ ] OpenWeather
- [ ] Refresh Wifi Connections 
- [ ] Disconnect Wifi 
- [ ] Docker integration
- [ ] Removable Drive Menu
- [ ] Sound input & output device chooser
- [ ] Sound Settings
- [ ] Status Area Horizontal Spacing 
- [ ] NoAnnoyance
- [ ] Remove Dropdown Arrows
- [ ] Screenshot Tool
- [ ] Tweaks in System Menu
- [ ] Touchpad indicator
- [ ] Places status indicator
- [ ] Bring Out Submenu Of Power Off/Logout Button 

### Bash RC File 

Open File:
```bash
sudo code ~/.bashrc
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


### Disk Partition Size

```
/dev/sda1   ntfs            Recuperação     530MB
/dev/sda2   fat32           /boot/efi       100MB
/dev/sda3   ms reserved                      16MB
/dev/sda4   ntfs            Windows10       160GB
/dev/sda5   ext4            /                30GB
/dev/sda6   ext4            /home            50GB
/dev/sda7   linux-swap                        6GB
```