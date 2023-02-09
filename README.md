# fedora_setup

for proper ffmpeg (good video playback outside YouTube on firefox and on desktop (?)
```
sudo dnf install https://download1.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm
sudo dnf install https://download1.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm
sudo dnf install -y ffmpeg
sudo dnf group upgrade --with-optional Multimedia
```

for signal desktop to launch in the tray
1.create autostart entry from tweak tool
2.edit autostart entry by navigating to .config/autostart/org.signal.Signal
3.edit the execution command by adding "start-in-tray" as such
```
/usr/bin/flatpak run --branch=stable --arch=x86_64 --command=signal-desktop --file-forwarding org.signal.Signal --start-in-tray @@u %U @@
```

check rpmfusion documentation for tips to install Virtualbox and other software
https://rpmfusion.org/Howto

For gnome-boxes (to enable high resolutions)
find this line in cofiguration, and increase video memory
```
<video>
      <model type='qxl' ram='65536' vram='65536' vgamem='16384' heads='1' primary='yes'/>
```

change it as shown
```
<video>
      <model type='qxl' ram='65536' vram='65536' vgamem='65536' heads='1' primary='yes'/>
```

Also inside guest windows machines install spice guest additions
https://www.spice-space.org/download.html
