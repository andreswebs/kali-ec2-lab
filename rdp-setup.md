# add a non-root user with `sudo` permissions

```sh
sudo addgroup --gid 2000 ec2-user
sudo adduser \
    --gid 2000 \
    --uid 2000 \
    --gecos "" \
    --disabled-login \
    ec2-user
sudo usermod -a -G sudo ec2-user
sudo passwd ec2-user
```

# install desktop

```sh
sudo apt install --yes kali-desktop-xfce

echo xfce4-session | sudo tee /home/ec2-user/.xsession

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
