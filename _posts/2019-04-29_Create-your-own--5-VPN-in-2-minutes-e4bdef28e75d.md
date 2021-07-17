---
title: Create your own $5 VPN in 2 minutes
---

![](/images/migrated/1__xYNBKqVzOa3kuBFNza0Ujw.jpeg)

Disclaimer: Goal of this guide is to introduce a lesser known feature of SSH. Readers are responsible for their own actions.

Well, it is not exactly a VPN but it gets the job done.

SSH is a well known secure way to access a remote computer over an unsecured network. SSH tunnelling or ssh port forwarding is a lesser known feature of ssh.

SSH tunnelling allows sending arbitrary network data through a secured SSH channel so that is encrypted and cannot be eavesdropped.

![](/images/migrated/1__7EomfYfi__TYzKztJQ__EkOQ.png)

### Step 1- create your server

Purchase your server

Head over to linode/Digitalocean and create an account. Create a new server. $5 droplet/linode is more than enough.

### Step 2 - Create ssh tunnel

Create a SSH tunnel from your computer to your server.

> ssh -D 8123 -f -C -N username@your-server-ip

### Step 3 - Set your proxy settings

Customize your proxy settings to 127.0.0.1:8123

![](/images/migrated/1__b0Zvlfkhjs3yqnjhpCsPdA.png)