# Ubuntu Visual Customizations.

### Setup Terminal Colors.

Pallette: XTerm

Text Default color: #FDE50E

Use transparent background: yes

### 1. GRUB
Background file is ../grub.png

`bash
sudo apt install grub-customizer
` 

### 2. Plymouth 
Custom boot screen installation:

````bash
sudo cp -r pisi-color/ /usr/share/plymouth/themes/

sudo update-alternatives --install /usr/share/plymouth/themes/default.plymouth default.plymouth /usr/share/plymouth/themes/pisi-color/pisi-color.plymouth 200
sudo update-alternatives --config default.plymouth
sudo update-initramfs -u
````

### 3. Linux Boot Screen

Remove 'quite splash' line as default boot option:
```bash
sudo vi /etc/default/grub
sudo update-grub2
```

### 4. Logon Background

Open css file:
```bash
sudo vi /usr/share/gnome-shell/theme/gdm3.css 
```

Please find and edit lines to match the following:
```css
#lockDialogGroup {
background: #2c001e url(file:////full/path/to/new/logon-screen.jpg);
background-repeat: no-repeat;
background-size: cover;
background-position: center;
}
```

### 5. XSCREENSAVER

Install and setup XScreensaver:
```bash
sudo apt remove gnome-screensaver
sudo apt install build-essential libsdl1.2-dev libsdl-ttf2.0-dev libsdl-gfx1.2-dev libx11-dev
git clone https://github.com/alexanderk23/gluqlo.git && cd gluqlo
make && sudo make install
sudo vi ~/.xscreensaver
```
 
Next add the line to the config config
```editorconfig
gluqlo -root \n\
```

Fix the bug that starts screensaver when video plays in full screen mode:
```bash
cd /usr/bin
sudo ln -s /home/exesse/Temp/Style/xscreensaver/xscreensaverstopper.sh xscreensaverstopper
```

From applications edit autostart and add new apps: 
```bash
NAME: XSCREENSAVER
RUN: xscreensaver -nosplash && xscreensaverstopper
```

### 6. XSECURELOCK

```bash
sudo apt install apache2-utils autoconf autotools-dev binutils gcc libc6-dev libpam-dev libx11-dev libxcomposite-dev libpam0g-dev libxext-dev libxfixes-dev libxft-dev libxmuu-dev libxrandr-dev libxss-dev make mplayer mpv pamtester pkg-config x11proto-core-dev xscreensaver
git clone https://github.com/google/xsecurelock.git
cd xsecurelock
sh autogen.sh
./configure --with-pam-service-name=xscreensaver
make && sudo make install
```

Create new key mapping to manually lock. On press 'super + L' run the command:
```bash
env XSECURELOCK_SAVER=saver_xscreensaver XSECURELOCK_PASSWORD_PROMPT=time_hex xsecurelock
```

### 7. Install Fonts

```bash
mkdir -p ~/.fonts/ && cp fonts/ ~/.fonts/
```


### 8. Install Theme

```bash
mkdir -p ~/.themes/ && cp -r themes/* ~/.themes/
```

### 9. Install Plank

```bash
sudo apt install plank
mkdir ~/.local/share/plank/themes/ -p && cp -r plank/* ~/.local/share/plank/themes/
sudo apt remove gnome-shell-extension-ubuntu-dock
```

And add to autostartup. 

### 10. Install Icons

```bash
mkdir -p ~/.icons/ && cp -r icons/* ~/.icons/
```

### 11. Install blyr from git repository:

```bash
git clone https://github.com/yozoon/gnome-shell-extension-blyr.git
cd gnome-shell-extension-blyr/
make local-install
```
Restart to enable the extension.

### Activete the themes
- Start gnome-tweaks and select 'Radvan*' in each respective category.
- In extensions set blyr to '10; 0.9; 1.00' for Activities + Panel.
- Select same theme for Plank.
