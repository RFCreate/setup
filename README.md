# Arch Installation

Follow the [installation guide](https://wiki.archlinux.org/title/Installation_guide#Pre-installation) in the Arch wiki to download the [ISO](https://wiki.archlinux.org/title/Installation_guide#Acquire_an_installation_image) and [verify the signature](https://wiki.archlinux.org/title/Installation_guide#Verify_signature).

---

Run the preinstallation script[^1] to copy the ISO to a **USB**<br>
<sub>**Note:** fill the USB and ISO variables for the script to run, also mkfs.fat and mkfs.ext4 need to be installed</sub>

```
curl -O https://raw.githubusercontent.com/shyguyCreate/setup/main/preinstall.sh
USB=/dev/your_usb
ISO=path/to/archlinux-version-x86_64.iso
. ./preinstall.sh
```

When finished, [boot into the USB](https://wiki.archlinux.org/title/Installation_guide#Boot_the_live_environment)

---

Inside the bootable USB, connect to [wireless internet](https://wiki.archlinux.org/title/Installation_guide#Connect_to_the_internet) using [iwctl](https://wiki.archlinux.org/title/Iwd#iwctl)

```
iwctl
[iwd]# device list                                # list wifi devices
[iwd]# device  _device_  set-property Powered on  # turn on device
[iwd]# adapter _adapter_ set-property Powered on  # turn on adapter
[iwd]# station _device_ scan                      # scan for networks
[iwd]# station _device_ get-networks              # list networks
[iwd]# station _device_ connect _SSID_            # connect to network
[iwd]# station device show                        # display connection state
[iwd]#  ( Ctrl+d )                                # exit
```

---

Run installation script[^1]<br>
<sub>**Note:** fill the DISK variable for the script to run</sub>

```
mkdir -p /root/usb
mount /dev/your_usb2 /root/usb
DISK=/dev/your_disk
. /root/usb/install.sh
```

---

[Change root into new system](https://wiki.archlinux.org/title/Installation_guide#Chroot)

```
arch-chroot /mnt
```

---

[Set the root password](https://wiki.archlinux.org/title/Installation_guide#Root_password)

```
passwd
```

---

Run setup script[^1]<br>
<sub>**Note:** to change username, modify variables inside the script</sub>

```
. /setup.sh > output.txt 2> error.txt
```

---

Set the user password<br>
<sub>**Note:** change shyguy with your username if you change it in the script</sub>

```
passwd shyguy
```

---

[Reboot the system](https://wiki.archlinux.org/title/Installation_guide#Reboot)

1. Exit chroot: `exit`
2. Unmount disk: `umount -R /mnt`
3. Reboot system: `reboot`

---

Connect to wireless internet using [Network Manger](https://wiki.archlinux.org/title/NetworkManager#Usage)

```
nmtui
```

[^1]: Script assumes that is running as root.
