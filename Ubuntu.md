#Enable Gnome VNC on Ubuntu 18.04
sudo apt-get update
sudo apt-get upgrade
sudo apt-get dist-upgrade
sudo apt-get install --no-install-recommends ubuntu-desktop
sudo apt-get install vino
sudo apt-get install dconf-editor
dconf-editor
ORG > GNOME > DESKTOP > REMOTE ACCESS
Require Encryption == OFF
sudo gsettings set org.gnome.Vino require-encryption false
sudo vi /etc/netplan/01-netcfg.yaml
renderer: NetworkManager
