# Visual Customizations. Working folder is /home/exesse/Temp/Style

# Setup Terminal Colors
# Pallette: XTerm
# Text Default color: #FDE50E
# Use transparent background: yes

# 1. GRUB
# Background file is ../grub.png 
sudo apt install grub-customizer

# 2. Plymouth 
# Custom boot screen installation:
sudo cp -r pisi-color/ /usr/share/plymouth/themes/
sudo update-alternatives --install /usr/share/plymouth/themes/default.plymouth default.plymouth /usr/share/plymouth/themes/pisi-color/pisi-color.plymouth 200
sudo update-alternatives --config default.plymouth
sudo update-initramfs -u

# 3. Linux Boot Screen
# Remove 'quite splash' for default boot
sudo vi /etc/default/grub
sudo update-grub2

# 4. Logon Background
sudo vi /usr/share/gnome-shell/theme/gdm3.css 
# next edit the line
; #lockDialogGroup {
; background: #2c001e url(file:////home/exesse/Temp/Style/logon-screen.jpg);
; background-repeat: no-repeat;
; background-size: cover;
; background-position: center;
; }

# 5. XSCREENSAVER
sudo apt remove gnome-screensaver
sudo apt install build-essential libsdl1.2-dev libsdl-ttf2.0-dev libsdl-gfx1.2-dev libx11-dev
git clone https://github.com/alexanderk23/gluqlo.git && cd gluqlo
make && sudo make install
sudo vi ~/.xscreensaver 
# add line to config
; gluqlo -root \n\
# destribute fix for autoscreen mode bug
cd /usr/bin
sudo ln -s /home/exesse/Temp/Style/xscreensaver/xscreensaverstopper.sh xscreensaverstopper
# add to autostart 
; XSCREENSAVER
; xscreensaver -nosplash && xscreensaverstopper

# 6. XSECURELOCK
sudo apt install apache2-utils autoconf autotools-dev binutils gcc libc6-dev libpam-dev libx11-dev libxcomposite-dev libpam0g-dev libxext-dev libxfixes-dev libxft-dev libxmuu-dev libxrandr-dev libxss-dev make mplayer mpv pamtester pkg-config x11proto-core-dev xscreensaver
git clone https://github.com/google/xsecurelock.git
cd xsecurelock
sh autogen.sh
./configure --with-pam-service-name=xscreensaver
make && sudo make install
# create key mapping to manually lock
; on press 'super + L'
; env XSECURELOCK_SAVER=saver_xscreensaver XSECURELOCK_PASSWORD_PROMPT=time_hex xsecurelock

# 7. Install Fonts
mkdir -p ~/.fonts/ && cp fonts/ ~/.fonts/

# 8. Install Theme
mkdir -p ~/.themes/ && cp -r themes/* ~/.themes/

# 9. Install Plank
sudo apt install plank
mkdir ~/.local/share/plank/themes/ -p && cp -r plank/* ~/.local/share/plank/themes/
sudo apt remove gnome-shell-extension-ubuntu-dock
# add to autostartup

# 10. Install Icons
mkdir -p ~/.icons/ && cp -r icons/* ~/.icons/

# 11. Install blyr from canonical PPA

# {7-11}
# Start gnome-tweaks
# Select 'Radvan*' in each respective category
# Select same for plan theme
# In extensions set blyr to '10; 0.9; 1.00' for Activities + Panel


