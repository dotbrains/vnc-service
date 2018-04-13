# VNC-Service

Service file to start TightVNC or TigerVNC as a service in Kali-Linux.

## Use

In order to use [`vncserver@.service`](vncserver@.service) you must download it into the `/lib/systemd/system` directory by using the follow snippet:

```
sudo wget -O /lib/systemd/system/vncserver@.service https://github.com/nicholasadamou/VNC-Service/raw/master/vncserver@.service && \
    sudo wget -O /usr/local/bin/start_tightvncserver https://github.com/nicholasadamou/VNC-Service/raw/master/start_tightvncserver && \
    sudo chmod +x /usr/local/bin/start_tightvncserver && \
    sudo systemctl enable vncserver@1.service && \
    sudo systemctl start vncserver@1.service
```

This service runs `vncserver` as `root`. This can be changed by modifying `/lib/systemd/system/vncserver@.service`.

## Allow Multiple Concurrent `xfce` Sessions

To allow multiple simultanious `xfce` sessions and fix the `xfce4-session: Another session manager is already running` error, run the following snippet:

```
wget -O ~/.vnc/xstartup https://github.com/nicholasadamou/VNC-Service/raw/master/xstartup && \
    sudo chmod 755 ~/.vnc/xstartup
```

## Note

The VNC server restricts connections from the localhost only for security reasons.

To connect to the vnc-server over the network use an ssh tunnel (this is assuming that your vnc-server is running on `172.20.10.4`: 

```
ssh -L 5902:localhost:5901 root@172.20.10.4
vncviewer 127.0.0.1::5902
```

However, since you are `ssh`'ing into your remote machine, you might as well just type `vncserver` and be done instead of running it as a service.

## License

The code is available under the [MIT license](LICENSE).