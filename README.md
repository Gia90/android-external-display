# NXD: aNdroid eXternal Display
Open source solution to use android devices as external display on linux.

## Configuration

### Main device (linux machine)
- x11 (x11vnc)
- adb
- [*optional*] arandr, needed for the repositioning functionality

### Secondary device (android device)
- sshd
- [bVNC](https://play.google.com/store/apps/details?id=com.iiordanov.freebVNC), or any VNC Client

## Issues
- No virtual display is found: `xrandr: cannot find output "VIRTUAL1"`  
The solution would be to create this file `/usr/share/X11/xorg.conf.d/20-intel.conf`  
with the following content:
```
Section "Device"
    Identifier "intelgpu0"
    Driver "intel"
    Option "VirtualHeads" "2"
EndSection
```
and the logout/re-login.

## Credits
- [linux-second-screen](https://github.com/brunodles/linux-second-screen)
