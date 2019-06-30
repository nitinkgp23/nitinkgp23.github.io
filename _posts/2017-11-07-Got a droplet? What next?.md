---
title: Got a droplet? What next?
excerpt: One of the various tutorials to help myself with repetitive tasks, such as getting a droplet on DO and configuring it.
date: 2017-11-07
categories:
 - tutorial
tags:
 - droplet
 - server
 - ubuntu
comments: true
---

# Getting the droplet

You can get a droplet on DigitialOcean at some minimal price. I got mine using the Github Student Pack, which gives an initial credit of 50 $. Below is explained well, the steps to follow just after you have got the server.

I will be using ssh-keys to login to the server, hence at the time of the creation of the droplet, I chose the option 'Use SSH Keys' and uploaded the content of the file id_rsa.pub present in ~/.ssh . This helped me avoid getting a password of the server through the email.

After completing the processes online, come back to the terminal and type:

```
ssh root@139.59.67.18
```

Replace the IP address with the server's IP address. This won't prompt you for a password if you have set up SSH as described above. (Also, make sure you are not behind a proxy or firewall.)

# Creating a sudo user on ubuntu

After ssh-ing into the server, the prompt becomes:

```
root@pascal ~ $ 
```

Follow this DigitalOcean [tutorial](https://www.digitalocean.com/community/tutorials/how-to-create-a-sudo-user-on-ubuntu-quickstart) to create a sudo user on the server. After following this tutorial, logout.

Now, we will allow the user login through ssh. For this, follow the steps:

1. Login to the server again using `root@139.59.67.18`.
2. `cat .ssh/authorized_keys`
    This will echo the contents of the file. Copy the contents.
3. `su - nitinkgp23`
    nitinkgp23 is the username of the sudo user that we created following the DO tutorial.
4. `mkdir .ssh && cd .ssh` : Create the folder and cd into it.
5. `touch authorized_keys` : Create the file.
6. Now, open the file using nano and paste the contents that you copied in Step 2.
7. `cd ~` : Come back to the home folder.
8. Provide proper permissions to the ssh file :
    ```
    chmod 700 .ssh
    chmod 664 .ssh/authorized_keys
    chown nitinkgp23:nitinkgp23 /home/nitinkgp23
    ```
9. Logout
10. You can login to the server now using username : `ssh nitinkgp23@139.59.67.18`

# Install and configure RealVNC to access GUI

Follow this [tutorial](https://www.digitalocean.com/community/tutorials/how-to-install-and-configure-vnc-on-ubuntu-16-04) to install RealVNC on your local computer and remote server.

On running the command `vncserver` on remote server, suppose you get the output `New 'X' desktop is your_server_name.com:1`

Keep note of the number `1` . Now, come back to local computer, start VNC-Viewer (Install it, if not installed already), and create a new connection. Give the IP address as `139.59.67.18:1` . Note the number appended at last is `1`. This will start the GUI access to the droplet.

# Workaround for proxy

