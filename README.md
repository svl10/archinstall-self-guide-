# archinstall-self-guide-

## Optional
```setfont -d``` to make font bigger

```pacman-key --init```
<br>
```pacman-key --populate archlinux```
<br>
```pacman -Sy or pacman -Sy archlinux-keyring```
<br>
```pacman -S archinstall```
<br>

```nano /etc/systemd/timesyncd.conf```
<br>
#uncomment "NTP=" and set it as "NTP=time.google.com"
<br>
```systemctl restart systemd-timesyncd```
<br>


__If it doesn't work then try to manually set timezone via timedatectl__
<br>
``` timedatectl set-timezone "Asia/Singapore" ``` #could also work for hong kong
<br>
You can now proceed to use archinstall


---
## Manual Install

### Connecting to Wi-Fi (Optional)
<br>

```
iwctl
device list
```

Run ```device devicename show``` devicename could be something like wlan0 <br>
``` station wlan0 get-networks``` to show available Wi-Fi networks <br>
To connect run ```station wlan0 connect Wi-FiName``` <br>
``` exit``` <br>
Run ``` ping www.google.com``` to check internet connection

---

To list available disk use <br>
```lsblk```
<br>
To select and partition disk <br>
```cfdisk </dev/thechoosendisk> ```
<br>
**Create 3 partitions for boot (100+Mb), root, and swap (4+Gb)**
<br>
To format the partition <br>
```mkfs.ext4 /dev/the_root_partition``` <br>
```mkfs.fat -F 32 /dev/the_boot_partition``` <br>
```mkswap /dev/swap_partition```<br>
**Mount the partitions** <br>
```mount /dev/root_partition /mnt ```
```
mkdir -p /mnt/boot/efi
mount /dev/boot_partition /mnt/boot/efi
```
```swapon dev/swap_partition ```

## Installing Packages
``` pacstrap -K /mnt base linux linux-firmware sof-firmware base-devel nano grub efibootmgr networkmanager ``` <br>
Could also add amd-ucode or intel-ucode depending on the CPU
<br>
## Genstab

```genfstab /mnt``` <br>
```genfstab /mnt > /mnt/etc/fstab``` <br>
*Check if it write* <br>
```cat /mnt/etc/fstab``` <br>

## Chroot

```arch-chroot /mnt ``` <br>

## Set Timezone
``` ln -sf /usr/share/zoneinfo/Region/City /etc/localtime ``` *Replace Region/City || mine is Asia/Singapore or Asia/Tokyo <br>
use ```hwclock --systohc``` to sync <br>
use ```date``` to check

## locale.gen
```nano /etc/locale.gen ``` remove # from chosen language .UTF-8 UTF-8 <br>
run ```locale.gen``` to generate <br>
create locale.conf by running ```nano /etc/locale.conf``` and input ```LANG=choosenlanguage.UTF-8 <br>

## Host Name
```nano /etc/hostname``` type whatever hostname you want 

## Root password
run ```passwd``` to set root password

## Adding User

```
useradd -m -G wheel -s /bin/bash username
passwd username
```

## Give a user access to sudo
make sure your in root, if not simply run ```exit``` to go back to root <br>
run ```EDITOR=nano visudo``` and uncomment or remove # %wheel ALL=(ALL) ALL from the bottom

## Enabling services through systemctl
```systemctl enable NetworkManager```

## Setting up Grub
```grub-install /dev/installeddisk```
```grub-mkconfig -o /boot/grub/grub.cfg```

## Reboot
Run ```exit``` to go back to live environment
```umount -a```
```reboot```
