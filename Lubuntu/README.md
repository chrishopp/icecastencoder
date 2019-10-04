# Lubuntu (Lubuntu 18.04.3 LTS last tested)
Lubuntu downloads, https://lubuntu.me/downloads/
1. Install Lubuntu with preferred options, see next 2 items
2. Install with minimal installation selected, do not install thirt-party software for graphics and Wi-Fi...; required items will be installed with required packages
3. As this is an ESXi based install guide, I will choose to log in automatically. If this is a standalone install you can require password to login and setup autologin and lock screen later similar to my Icecast install guide.
4. Run an initial system update (important for updating dependencies)
```
sudo apt-get update
sudo apt-get upgrade
```
## Install a few useful utilities (if needed)
1. openssh-server for future remote acess if desired
```
sudo apt-get install openssh-server
```
2. open-vm-tools (if VM install)
```
sudo apt-get install open-vm-tools-desktop
```
3. notepadqq (not needed for command line only install)
```
sudo apt-get install snapd
sudo snap install notepadqq --devmode
```
to run notepadqq in root, sudo notepadqq --allow-root
## uninstall/blacklist onboard devices (if needed)
1. If using a sound card, disable on-board sound in BIOS, if can't, blacklist sound devices that aren't your preffered device, multiple sound devices make working with audio inputs difficult
2. discover sound device names
```
nano /proc/asound/modules
```
3. add extra device(s) to a blacklist file, i.e. "0 snd_hda_intel" from  modules
```
sudo notepadqq /etc/modprobe.d/sound.blacklist.conf
```
4. add the following line
```
blacklist snd_hda_intel
```
## Download latest source files and extract
1. https://sourceforge.net/projects/butt/
2. Extract to preferred location and from extracted folder open terminal
3. install butt dependancies (some items may vary based on encoding needs, aac, mp3, etc.)
```
sudo apt-get install portaudio19-dev libvorbis-dev libfltk1.3-dev libmp3lame-dev libflac-dev libsamplerate-dev libopus-dev fdkaac libfdk-aac-dev libogg-dev libdbus-1-dev libsamplerate0-dev
```
4. configure and install butt running terminal from butt extracted folder
```
sudo ./configure
sudo make
sudo make install
```
5. launch butt for the first time to create first config file in /home/[user] (file is hidden)
```
butt
```
## Configure butt configuration file as needed, copy as needed and rename and reconfigure for multiple instances
## Useful extras
1. purge light-locker and install xscreensaver (light-locker turns off audio on screensaver lock/screen lock)
https://askubuntu.com/questions/450443/light-locker-stops-background-activities-eg-music-playback-when-screen-is-loc
```
sudo apt-get purge light-locker light-locker-settings
sudo apt-get install xscreensaver
```
2. setup autolock after login (allows butt to startup gui interface, then locks instance)
```
sudo notepadqq /home/[user]/Documents/lock.sh
```
make the content of the file as follows:
```
sleep 10
xscreensaver & -nosplash
sleep 1
xscreensaver-command -lock
```
chmod +x file to allow it to execute
```
sudo chmod +x /home/[user]/Documents/lock.sh
```
3. edit autostart file to include all butt configs and autolock file
```
sudo notepadqq /home/[user]/.config/lxsession/Lubuntu/autostart
```
give file following content, each butt line with 1 config
```
butt -c /home/[user]/.buttrc-aac & disown
butt -c /home/[user]/.buttrc-aacmobile
butt -c /home/[user]/.buttrc-mp3
butt -c /home/[user]/.buttrc-mp3test
```
add screen lock line if desired
```
bash /home/[user]/Documents/lock.sh
```
4. mount a network share where your playlist updates for nowplaying information integrated into the stream, currently only title is supported with Icecast, shoutcast has some more, ogg/vorbis has even more, title is about all that works most places reliably though
```
sudo apt-get install cifs-utils
```
make now playing mountpoint locally
```
sudo mkdir /mnt/nowplaying
sudo chown -R [user]:root /mnt/nowplaying
sudo chmod -R 0770 /mnt/nowplaying
```
create smbcredentials file in user folder
```
notepadqq ~/.smbcredentials
```
make content as follows
```
username=user
password=password
```
edit file permissions
```
chmod 600 ~/.smbcredentials
```
5. edit fstab file to automount this location
```
sudo notepadqq /etc/fstab --allow-root
//[machine name]/nowplaying /mnt/nowplaying cifs credentials=/home/[user]/.smbcredentials,gid=1000,file_mode=0770,dir_mode=0770,iocharset=utf8 0 0
```
mount to test things out
```
sudo mount -a
```
now you can use the location /mnt/nowplaying in your config file for butt under the stream>update song name from file option
## Future
1. Script entire process
2. Describe configuration file setup in detail
3. Shell only guide and hints
