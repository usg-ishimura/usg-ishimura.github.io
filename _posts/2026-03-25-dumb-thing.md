---
author: Alessandro Ideo
github_username: usg-ishimura
tags: hacking
image: https://github.com/user-attachments/assets/aa34c041-5014-4da5-894b-8cbde23bc6f1
---
# Fixing DHCP Failure on Raspberry Pi Zero 2 W with USB Gadget Mode (IoT Hacking Lab)

I recently purchased a raspberry pi zero 2W specifically to follow the IoT and hardware hacking blog post series at [<ins>https://tcm-sec.com/getting-started-with-iot-hardware-hacking/</ins>](https://tcm-sec.com/getting-started-with-iot-hardware-hacking/). My setup includes a Rasbperry Pi with male header pins soldered to the board, a 32GB micro SD card, a USB to micro USB data cable, female to female jumper wires, a UART to USB adapter and my Debian Notebook.

Here a picture of my setup:

![Setup Image 2026-03-25 at 20 01 33](https://github.com/user-attachments/assets/aa34c041-5014-4da5-894b-8cbde23bc6f1)


After flashing the "Dumb Thing" vulnerable IoT firmware onto a Raspberry Pi Zero 2 W and configuring `/etc/wpa_supplicant.conf` to join my home network via UART shell, the Pi failed to obtain a DHCP lease and fell back to an APIPA address. The Pi successfully associated with a hotspot, visible in the connected devices list with its MAC address, but no IP was ever assigned via DHCP. Configuring a static IP manually did not help either, as ARP requests to the gateway went unanswered (`<incomplete>`), preventing any L2 communication between the Pi and the rest of the network. To work around this, I enabled USB OTG by loading the `dwc2` and `g_ether` kernel modules, then connected the Pi to my PC via a USB data cable (micro-USB port, not PWR IN), which exposed a `usb0` network interface on both ends. This allowed me to reach the Pi's web server directly over USB without relying on WiFi at all.

### Find the boot partition device
```sh
cat /proc/partitions
```

### Then mount the FAT32 partition (usually mmcblk0p1)
```sh
mkdir -p /mnt/boot
mount /dev/mmcblk0p1 /mnt/boot
```

### Verify
```sh
ls /mnt/boot
cat /mnt/boot/config.txt
```

### Add dwc2 to config
```sh
echo "dtoverlay=dwc2" >> /mnt/boot/config.txt
```

### Create a script in /etc/init.d/ that loads the dwc2 and g_ether kernel modules
```sh
cat > /etc/init.d/S99usbgadget << 'EOF'
#!/bin/sh
modprobe dwc2
modprobe g_ether
EOF
```

### Make the init script executable
```sh
chmod +x /etc/init.d/S99usbgadget
```

### Then reboot
```sh
reboot
```

### Set Pi zero static IP on usb0 and bring the new interface up
```sh
ip addr add 192.168.7.2/24 dev usb0
ip link set usb0 up
```

On your PC, assign `192.168.7.1/24` to the USB interface that appears (you can omit the gateway), then open your browser to `http://192.168.7.2`, the UI for interacting with the firmware will show up and you will be able to perform your pentest on "Dumb Thing" following the free resources [<ins>here</ins>](https://tcm-sec.com/getting-started-with-iot-hardware-hacking/)

**Happy hacking!**
