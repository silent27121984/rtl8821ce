# Realtek RTL8821CE Driver for WiFi TP-Link AC600 Archer T2E(EU) Ver:1.0 PCI

#### Installing driver from Linux mint

```
git clone https://github.com/silent27121984/rtl8821ce.git
```
```
cd rtl8821ce
```
```
sudo ./dkms-install.sh
```
```
sudo reboot
```
## Possible issues

#### PCIe Activate State Power Management
Your distribution may come with PCIe Active State Power Management enabled by default. That may conflict with this driver. To disable:

```
sudo nano /etc/default/grub
```
Add pci=noaer at the end of GRUB_CMDLINE_LINUX_DEFAULT. Line should look like this:

```
GRUB_CMDLINE_LINUX_DEFAULT="quiet splash pci=noaer"
```

Then update your GRUB configuration:
```
sudo update-grub
```
```
sudo reboot
```
### Secure Boot

If your system uses Secure Boot, disable it via BIOS settings, otherwise the kernel will not accept user-supplied modules.

Then, just reboot or restart the NetworkManager unit to fix the problem.

### Wi-Fi not working for kernel >= 5.9
The Linux Kernel 5.9 version comes with a broken `rtw88` module developed by Realtek that has poor compatibility with most revision of the 8821ce chip.

You must disable it by adding the following to your module blacklists (`/etc/modprobe.d/blacklist.conf`):
```
sudo nano /etc/modprobe.d/blacklist.conf
```
```
blacklist rtw88_8821ce
```
```
sudo reboot
```
