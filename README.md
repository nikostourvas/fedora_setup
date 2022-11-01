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
