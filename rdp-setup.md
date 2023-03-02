# add a non-root user with `sudo` permissions

```sh
sudo addgroup --gid 2000 kali
sudo adduser \
    --gid 2000 \
    --uid 2000 \
    --gecos "" \
    --disabled-login \
    kali
sudo usermod -a -G sudo kali
sudo passwd kali
```

# install desktop

```sh
sudo apt update
sudo apt install --yes kali-desktop-xfce

echo xfce4-session | sudo tee /home/kali/.xsession

cat <<EOF | sudo tee /etc/polkit-1/localauthority/50-local.d/45-allow-colord.pkla
[Allow Colord all Users]
Identity=unix-user:*
Action=org.freedesktop.color-manager.create-device;org.freedesktop.color-manager.create-profile;org.freedesktop.color-manager.delete-device;org.freedesktop.color-manager.delete-profile;org.freedesktop.color-manager.modify-device;org.freedesktop.color-manager.modify-profile
ResultAny=no
ResultInactive=no
ResultActive=yes
EOF
```

# install xrdp

```sh
sudo apt install --yes xrdp
sudo systemctl start xrdp
sudo systemctl enable xrdp
```
