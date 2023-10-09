# fedora_setup

for proper ffmpeg (good video playback outside YouTube on firefox and on desktop (?)
```
sudo dnf install https://download1.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm
sudo dnf install https://download1.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm
sudo dnf install -y ffmpeg
sudo dnf group upgrade --with-optional Multimedia
```

if running Fedora Silverblue check this page:
https://rpmfusion.org/Howto/OSTree

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

Using tlp
If you’re going to use TLP, please stop, disable and then mask GNOME power profiles to avoid any issues with conflicts.

sudo systemctl stop power-profiles-daemon.service

sudo systemctl disable power-profiles-daemon.service

sudo systemctl mask power-profiles-daemon.service


This will stop the service until you decide to unmask it again. Please remove TLP first, then re-enable/unmask power profiles.

sudo systemctl enable power-profiles-daemon.service

sudo systemctl start power-profiles-daemon.service

sudo systemctl unmask power-profiles-daemon.service

check tlp setting with 
```sudo tlp-stat -p```

and edit settings with
```sudo vim /etc/tlp.conf```

## docker post-install on silverblue
copy the line about docker from /usr/lib/group to /etc/groups
add username to the end of this line in /etc/groups

## vim mode in terminal
add to .bashrc
```set -o vi```

## modern csv editor install
create a distrobox container with
```distrobox create -i ubuntu:22.04 -n test```

you need to install GUI dependencies
unfortunately modern csv installer does not do that!
a quick and dirty way to achieve this is to install some other KDE application, for example:
```sudo apt install okular```

go to modern csv directory and install it
``` sudo sh install.sh```

export app to host system
```distrobox-export --app moderncsv```

## amd p-state driver in amd zen 3 laptops
firsly disable acpi_cpufreq driver
```
sudo grubby --args=initcall_blacklist=acpi_cpufreq_init --update-kernel=ALL
```

secondly, enable p-state (passive or active, more options to come in next version of linux kernel)
```
sudo grubby --update-kernel=ALL --args="amd_pstate=passive"
```
To revert changes use the option --remove-args instead of --args

## amd p-state_epp driver in kernel 6.5
Check available epp states
```
cat /sys/devices/system/cpu/cpu0/cpufreq/energy_performance_available_preferences
```

set epp state
```
echo "balance_performance" | sudo tee /sys/devices/system/cpu/cpu*/cpufreq/energy_performance_preference
```

## Disable amd-pstate-epp
```
sudo grubby --args=initcall_blacklist=amd_pstate_init --update-kernel=ALL
```

Revert it with:
```
sudo grubby --remove-args=initcall_blacklist=amd_pstate_init --update-kernel=ALL
```

## hp scanners
"Simple-Scan" cannot detect scanners on silverblue. Install simple-scan inside a distrobox 
```
sudo apt update
sudo apt install simple-scan hplip
```
then expose the application to the host system. From the distrobox terminal type:
```
distrobox-export -app simple-scan
```

## CapsLock as Esc in VS CODE
Click the gear icon --> settings --> search for "keyboard.dispatch"
Set it to the KeyCode option
