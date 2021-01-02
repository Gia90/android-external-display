# NXD: aNdroid eXternal Display
Open source solution to use android devices as external display on linux.

## Requirements

### Main device (linux machine - server)
- x11 (x11vnc) (_xorg only for now, sorry wayland users_)
- [adb](https://developer.android.com/studio/command-line/adb)
- [_optional_] arandr, needed to be able to move the display around

### Secondary device (android device - client)
- [termux](https://termux.com/)
- [sshd](https://wiki.termux.com/wiki/Remote_Access#Using_the_SSH_server)
- [bVNC](https://play.google.com/store/apps/details?id=com.iiordanov.freebVNC) (or any other VNC Client that handles "vnc://" links)

## How to use NXD
1. Start the SSH server on the android client. In termux, run: `sshd`.
1. Be sure to be able to successfully connect to the it from the linux machine: `ssh {CLIENT_IP} -p 8022`. If not, setup a secure authentication method ([guide](https://wiki.termux.com/wiki/Remote_Access#OpenSSH)).
1. Connect the android client to the linux machine through `adb` ([guide](https://wiki.lineageos.org/adb_fastboot_guide.html))
  1. [Advanced]: you can even connect them through adb wirelessly: `adb connect {CLIENT_IP}`
1. Be sure that the android device is unlocked and execute NXD: `./nxd`

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
