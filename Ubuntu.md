echo 'Acquire::http::Proxy "http://proxy.com.cn:80";' | sudo tee /etc/apt/apt.conf

export http_proxy="http://proxy.com.cn:80"
export https_proxy="https://proxy.com.cn:80"
export no_proxy="localhost,127.0.0.1"

sudo apt-get upgrade
sudo apt-get dist-upgrade
sudo apt-get install --no-install-recommends ubuntu-desktop

sudo apt install -y xrdp
sudo sed -e 's/^new_cursors=true/new_cursors=false/g' -i /etc/xrdp/xrdp.ini
sudo systemctl restart xrdp

DT=/usr/share/ubuntu:/usr/local/share:/usr/share:/var/lib/snapd/desktop
cat <<EOF > ~/.xsessionrc
export GNOME_SHELL_SESSION_MODE=ubuntu
export XDG_CURRENT_DESKTOP=ubuntu:GNOME
export XDG_DATA_DIRS=${DT}
export XDG_CONFIG_DIRS=/etc/xdg/xdg-ubuntu:/etc/xdg
EOF

cat <<EOF | sudo tee /etc/polkit-1/localauthority/50-local.d/xrdp-color-manager.pkla
[Netowrkmanager]
Identity=unix-user:*
Action=org.freedesktop.color-manager.create-device
ResultAny=no
ResultInactive=no
ResultActive=yes
EOF

sudo systemctl restart polkit
