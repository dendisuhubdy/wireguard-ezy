# WireGuard-ezy

Simplified installation of a [WireGuard](https://www.wireguard.com/) server for Ubuntu (tested on Ubuntu 20.04; should work on 18.04 as well. WireGuard is a Virtual Private Network (VPN) system which is new, fast, and claims to be secure. Unfortunately, it's also rather complex to install, and the documentation is highly technical. That's why we've prepared this script and step-by-step guide.

This script will set up a server, and will also create client configurations for as many clients as you want. Each device that will connect will need a separate configuration. Note that client devices will be able to see each other on the VPN, as well as the server.

To install:

    curl https://raw.githubusercontent.com/fastai/wireguard-ezy/master/wireguard-ezy.sh | sudo bash

## Questions during installation

You will need to answer the following three questions:

### Use VPN for *all* internet traffic? [y/n]

If this VPN is just so that the clients can see each other and the server, respond **n**. If you want *all* traffic to route via the VPN (e.g. to change your apparent location, or to increase privacy and security), respond **y**.

### \# of clients? \[Betwen 1 and 253]

Each device that will need to connect to your VPN is a *client*, and needs a separate configuration file. There's no real downside to creating more client configuration files than you end up using, so err on the high side when answering this question. (E.g. if you're just planning to use this yourself for watching foreign media, you might later find friends and family members wanting to use it too...)

You can always add more clients later, but it's simpler to do it during installation.

### Server hostname/IP?

This is the host name or IP address that you are installing the server on. The default is to use the current public IP address, by getting the output from the [ifconfig.me] service. If your server IP is not static, you'll need to use dynamic DNS to get a host name that you can connect to, and you should enter the host name here instead of the IP address.

Generally, it's better to use a hostname than an IP if possible, since if you later need to move your VPN server, you can always just update DNS to point the hostname at the new IP, instead of having the update all client configuration files on all devices.

## Connecting clients

The server will be running as soon as the script is complete, and the details of the server IP address (which will be set to `10.42.42.1`) will be printed to confirm success. The server will also be automatically run on reboot, and will reconnect automatically if there are any network issues.

In directory you run the script, you will find a `clients.zip` file. This contains the client configuration files you requested. Give one to each person/device that needs to connect, and keep a list somewhere of which numbered config you give to which client, so if you need to remove or re-assign it later, you know who is who. On each device, the user will need to install the WireGuard software from [here](https://www.wireguard.com/install/), and will then follow the directions below.

### Windows

1. Click Start, then type "wireguard" and press enter (or click the WireGuard icon)
1. Click "Add Tunnel" (or press <kbd>Ctrl</kbd><kbd>O</kbd>
1. Choose your config file
1. Click *Activate*

### Mac

I don't have a Mac to test with, so I'm copying the directions from [Mullvad](https://mullvad.net/en/help/wireguard-macos-app/):

1. Click on the WireGuard icon located in your desktop's top menu bar.
1. In the drop-down menu, select Import tunnel(s) from file...
1. Navigate to your Download folder and select the configuration file.
1. Click Import.
1. Click Allow if you get a pop-up saying "'WireGuard' would like to Add VPN Configurations."
1. Click on the WireGuard icon located in your desktop's top menu bar.
1. In the drop-down menu, select the server that you just imported
1. A checkmark will appear next to it. That's it!
