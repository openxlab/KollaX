#Enable Gnome VNC on Ubuntu 18.04
sudo apt-get update
sudo apt-get upgrade
sudo apt-get dist-upgrade
sudo apt-get install --no-install-recommends ubuntu-desktop
sudo apt-get install conf-editor
dconf-editor
ORG > GNOME > DESKTOP > REMOTE ACCESS
sudo vi /etc/netplan/01-netcfg.yaml
renderer: NetworkManager
