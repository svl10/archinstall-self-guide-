# archinstall-self-guide-

Auto(archinstall):

pacman-key --init 
<br>
pacman-key --populate archlinux
<br>
pacman -Sy or pacman -Sy archlinux-keyring
<br>
pacman -S archinstall
<br>

nano /etc/systemd/timesyncd.conf
<br>
#uncomment "NTP=" and set it as "NTP=time.google.com"
<br>
systemctl restart systemd-timesyncd
<br>


#If it doesn't work then try to manually set timezone via timedatectl
<br>
timedatectl set-timezone "Asia/Singapore" #could also work for hong kong
<br>
#Now try running archinstall
