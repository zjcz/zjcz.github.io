---
layout: post
title: "Installing Samba on Linux Mint"
date: 2025-06-16 11:07:00
categories: linux
tags: [linux, samba]
---

I recently setup a Samba share on my Linux Mint system to allow file sharing with other devices on my network. This post outlines the steps I took to install and configure Samba, create a user and group, set up the share directory, and ensure everything is working correctly. 

<!--more-->

While it is possible to do this in the UI, I prefer to do it via the command line for better control and understanding of the process. This guide assumes you have a basic understanding of Linux commands and have administrative access to your Linux Mint system.

This guide should work on any Debian-based distribution, including Ubuntu and its derivatives.

## Install and Configure

First, lets check everything is up to date:

```bash
sudo apt update && sudo apt upgrade -y
```

Now, install Samba:

```bash
sudo apt install samba
```

We now need to edit the Samba config file to set up the share. Open the Samba configuration file in a text editor.  You can use `nano` or any other text editor of your choice:

```bash
sudo nano /etc/samba/smb.conf
```

Add the following to the end of the file:

```ini
[share]
# This share requires authentication to access
path = /srv/samba/share/
read only = no
inherit permissions = yes
```

This will create a share named `share` that points to the directory `/srv/samba/share/` (we will create this folder later). The `read only = no` line allows users to write to the share, and `inherit permissions = yes` ensures that new files created in the share inherit the permissions of the directory.

## Create the Samba User and Group

Now we need to create a user and group for Samba. This user will be used to access the shared directory.  

Create a new user called `shareUser` (with no home directory and no login shell):

```bash
sudo useradd -M -s /sbin/nologin shareUser
```

Set a password for the user:

```bash
sudo passwd shareUser
```

Next, we need to add this user to Samba's user database. This allows the user to authenticate when accessing the Samba share.  When prompted, set a password for the Samba user. This can be the same as the system user password or different, depending on your preference.

```bash
sudo smbpasswd -a shareUser
```

Next, we create a user group for the Samba share. This group will be used to manage access to the shared directory.

```bash
sudo groupadd shareGroup
usermod -aG shareGroup shareUser
```

### Create the share directory

Create the directory for the share.  This is where the files will be stored that you want to share over the network:

```bash
sudo mkdir -p /srv/samba/share/
```

Change the ownership and permissions of the share directory:

```bash
sudo chgrp -R shareGroup /srv/samba/share/
sudo chmod 2770 /srv/samba/share/
```

## Restart Samba Service

After making changes to the Samba configuration file, you need to restart the Samba services to apply the changes:

```bash
smbd
```

## Test the Samba Configuration

To ensure that your Samba configuration is correct, run the following command:

```bash
testparm -s
```

## All Done

You should now be able to access the Samba share from other devices on your network. You can do this by entering the following in the file manager of another Linux machine or Windows machine:

```
\\<your-linux-mint-ip-address>\share
```

or alternatively you can use the `smbclient` command from the terminal:

```bash
smbclient -U shareUser //your-linux-mint-ip-address/share 
```

## Troubleshooting

If you run into problems accessing the share, here are some common troubleshooting steps:

### Check Network Connectivity

Ensure that your Linux Mint machine is connected to the network and that you can ping it from other devices.

### Allow Samba through the firewall

This one always gets me! If you have a firewall enabled, you need to allow Samba traffic. If you're using UFW (Uncomplicated Firewall), you can do this with the following command:

```bash
sudo ufw allow Samba
```

### Check the Samba Service Status
To check if the Samba service is running, you can use the following command:

```bash
sudo systemctl status smbd
```

If the service is not running, you can start it with:

```bash
sudo systemctl start smbd
```

Check for any errors on startup.

### Check the logs
If you encounter any issues, you can check the Samba logs for more information. The logs are typically located in `/var/log/samba/`. You can view the log files using:

```bash
sudo less /var/log/samba/log.smbd
```

### Discovering the Share

If you want the share to be discoverable by other devices on the network, consider investigating and using services such as `avahi-daemon` and `wsdd-service`.

## Further Reading

- [Samba Wiki - Setting up Samba as a Standalone Server](https://wiki.samba.org/index.php/Setting_up_Samba_as_a_Standalone_Server)
- [Linux Mint Forums - Share Folders using Samba in Home Network with Mint 21](https://forums.linuxmint.com/viewtopic.php?t=377372)
- [Ask Ubuntu - UFW firewall still blocking SMB despite adding rules](https://askubuntu.com/questions/36608/ufw-firewall-still-blocking-smb-despite-adding-rules)
