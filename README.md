# fedora_setup

for proper ffmpeg (good video playback outside YouTube on firefox and on desktop (?)
```
sudo dnf install https://download1.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm
sudo dnf install https://download1.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm
sudo dnf install -y ffmpeg
sudo dnf group upgrade --with-optional Multimedia
```

