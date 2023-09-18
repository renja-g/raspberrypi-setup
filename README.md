# Setup Raspberry Pi Without Monitor or Keyboard from a Windows Machine

## Table of Contents

- [Install Raspbian](#install-raspbian)
- [Connect to Raspberry Pi through SSH](#connect-to-raspberry-pi-through-ssh)
- [Update and Upgrade Raspberry Pi](#update-and-upgrade-raspberry-pi)
- [Configure Raspberry Pi](#configure-raspberry-pi)
- [Docker Setup](#docker-setup)

## Install Raspbian

- Install Raspbian with [Raspberry Pi Imager](https://www.raspberrypi.org/documentation/installation/installing-images/).
- [Set up wireless networking headless](https://www.raspberrypi.org/documentation/configuration/wireless/headless.md)
- [Enable SSH](https://www.raspberrypi.org/documentation/remote-access/ssh/README.md) on your Pi by placing a file name `ssh` (without any extension) onto the boot partition of the SD card.
- Insert the SD card into Raspberry Pi, plug in the power cord and network cable, and then power on the Pi.

## Connect to Raspberry Pi through SSH

First, you need to know the IP address of the Pi. You can find out the IP address from your router's administrator page (usually, it can be accessed by browsing http://192.0.0.1 from any machine inside your home network).
If you cannot find out the IP address from the router's administrator page, you can use [Advanced IP Scanner](http://www.advanced-ip-scanner.com/) to get the IP address.

After you get the IP address, you can use [PuTTY](http://www.putty.org/) to connect to your Raspberry Pi through SSH.
If the SSH connection is successful, you will be greeted with the login prompt of your Raspberry Pi.
Since it is your first login, you just need to input `pi` as user name and `raspberry` as password.

## Update and Upgrade Raspberry Pi

It is better to update Raspbian after your first login to your Pi.

```bash
sudo apt update
sudo apt full-upgrade
```

Per [here](https://www.raspberrypi.org/documentation/raspbian/updating.md) suggested, that `full-upgrade` is used in preference to a simple `upgrade`, as it also picks up any dependency changes that may have been made.

If your SD card is running out of space, your can free up some space with `sudo apt-get clean`. It will delete the downloaded package files (.deb files) from `/var/cache/apt/archives`.

## Configure Raspberry Pi

After you log into the Pi, type the following command to open the Raspberry Pi configuration UI.

```bash
sudo raspi-config
```

Make the following configurations:

- Expand file system to ensure that all of the SD card storage is available to the OS.

  `Advanced Options > Expand Filesystem`

- Enable VNC if needed

  `Interfacing Options > VNC > YES`


## Docker Setup

### Install Docker

```bash
curl -sSL https://get.docker.com | sh
```

```bash
sudo apt-get install -y uidmap
```

```bash
dockerd-rootless-setuptool.sh install
```

### Install docker-compose

```bash
sudo apt install python3-pip
```

```bash
sudo pip3 install docker-compose
```

### Docker login

```bash
docker login -u [username]
```
