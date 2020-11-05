# Guide to sucessfully setup a new Linux installation and get Eve Online installed + running with excellent performance

Assumption:
1. You use a fairly recent Linux distro based on Ubuntu (ex. POP!_OS, Mint, etc). Most of the steps may have already been done by you or pre-done by the OS.
2. Installation may require a few steps but you only need to do this once to have a fully working gaming system.

## 1 - Installation of 

For this guide, we will make use of [Lutris](https://lutris.net/).

## Install Lutris with the following command
```
sudo add-apt-repository ppa:lutris-team/lutris
sudo apt update
sudo apt install lutris
```

## Enable 32-bit libraries
```
sudo dpkg --add-architecture i386 
```

## Install [WINE](https://www.winehq.org/)
```
wget -nc https://dl.winehq.org/wine-builds/winehq.key
sudo apt-key add winehq.key
sudo add-apt-repository 'deb https://dl.winehq.org/wine-builds/ubuntu/ focal main' -y
sudo apt update
sudo apt-get install --install-recommends winehq-staging -y
sudo apt-get install libgnutls30:i386 libldap-2.4-2:i386 libgpg-error0:i386 libxml2:i386 libasound2-plugins:i386 libsdl2-2.0-0:i386 libfreetype6:i386 libdbus-1-3:i386 libsqlite3-0:i386 -y
```

## Grahphics Card Driver Install

### AMD Mesa Driver Install + Vulkan
```
sudo add-apt-repository ppa:kisak/kisak-mesa -y
sudo apt update
sudo apt install libgl1-mesa-dri:i386 mesa-vulkan-drivers mesa-vulkan-drivers:i386 -y
```

### Nvidia Proprietary Driver Install
```
sudo add-apt-repository ppa:graphics-drivers/ppa -y
sudo apt update
sudo apt install nvidia-driver-450 libnvidia-gl-450 libnvidia-gl-450:i386 libvulkan1 libvulkan1:i386 -y
```

## Valve's ACO Shader Compiler
Add this to /etc/environment:
```
RADV_PERFTEST=aco
```

## Esync
What is Esync?
Esync removes wineserver overhead for synchronization objects. This can increase performance for some games, especially ones that rely heavily on the CPU.

Check to see if esync is enabled already (most distributions do by default)
```
ulimit -Hn
```

If this returns more than 500,000 than ESYNC IS ENABLED! If not, proceed with these instructions:
Change the following files and add this line to the bottom of /etc/systemd/system.conf & /etc/systemd/user.conf
```
DefaultLimitNOFILE=524288
```

