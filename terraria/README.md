# Overview

This directory contains the configuration files that I use to run a Terraria server on Linux through Docker compose.
It is recommended that you change the password in the [configuration file](./serverconfig.txt) before starting the server.
To start the server, run:

```
docker compose up -d
```

All world data is saved in a Docker volume to persist across restarts.
Docker names the volume `terraria_data` and you can find the mountpoint using:

```
docker volume inspect terraria_data
```

You can debug the container by using a bash shell while no other container is running:

```
docker compose run --rm -it --entrypoint /bin/bash terraria
```

See the [Dockerfile](./Dockerfile) for the command that the container uses to run the server.

## WSL 2

If you want to run this in WSL 2 and connect locally, you need to run the following commands to add firewall rules and a network proxy from an Administrative Powershell:

```
netsh advfirewall firewall add rule name="Terraria WSL2" dir=in action=allow protocol=TCP localport=7777
netsh advfirewall firewall add rule name="Terraria WSL2" dir=in action=allow protocol=UDP localport=7777
netsh interface portproxy add v4tov4 listenaddress=0.0.0.0 listenport=7777 connectaddress=(wsl hostname -I).Split()[0] connectport=7777
```

You can view the active configurations via the following commands:

```
netsh advfirewall firewall show rule name="Terraria WSL2"
netsh interface portproxy show v4tov4
```

To delete them, run the following:

```
netsh advfirewall firewall delete rule name="Terraria WSL2"
netsh interface portproxy delete v4tov4 listenaddress=0.0.0.0 listenport=7777
```
