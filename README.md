# archinstall-self-guide-

Auto(archinstall):

pacman-key --init
pacman-key --populate archlinux
pacman -Sy or pacman -Sy archlinux-keyring
pacman -S archinstall

nano /etc/systemd/timesyncd.conf
#uncomment "NTP=" and set it as "NTP=time.google.com"
systemctl restart systemd-timesyncd


#If it doesn't work then try to manually set timezone via timedatectl
timedatectl set-timezone "Asia/Singapore" #could also work for hong kong

#Now try running archinstall
