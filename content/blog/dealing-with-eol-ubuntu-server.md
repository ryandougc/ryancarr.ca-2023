---
author:
  name: "Ryan Carr"
date: 2023-12-06
linktitle: Dealing with EOL Ubuntu Server
type:
- post
- posts
title: Dealing With EOL Ubuntu Server
weight: 10
series:
- Hugo 101
---

I’ve been running my personal website on an Ubuntu server for some time now. I created it with the latest version of Ubuntu Server OS at the time, which happened to be 22.10. I was unaware of the support lengths for the different versions. As it turns out, Ubuntu xx.10 is the “latest and greatest” version and therefore is not supported for more than a short, specified amount of time. It's no surprise that the server is now outdated and no longer supported.

This is a problem because I can no longer install new repos. I can no longer update any repos. I can no longer upgrade any software. Even if I want to upgrade to the newest experimental version of 23.10, the installation for this requires that I update and upgrade my current server first. 

After creating a ticket with my server host for their recommendation on what to do next, they gave me two options:

1. Migrate to Ubuntu Server 22.04. Technically a downgrade. 
2. Change the update servers that my server looks to when running commands like `apt update` and `apt upgrade`

I decided to go with option #1 because option #2 is a sort of workaround. The OS is still no longer supported and will not have any more security updates. 

### Migrating from Ubuntu server 22.10 to 22.04

Migrating servers is the process of transferring all of the data from one server to another server. In my case, since I am technically downgrading the OS from 22.10 to 22.04, I will set up a new server running Ubuntu Server 22.04 and then transfer all my files over from the old server running 22.10. 

There are some very clear [guides](https://www.digitalocean.com/community/tutorials/how-to-migrate-linux-servers-part-1-system-preparation) that were written by the people at Digital Ocean, my server host, which I will be following and I will be documenting my process along the way. Despite this guide being on Digital Ocean’s blog, they write in a very platform-agnostic manner and don’t expect that you are running your server on their services. I recommend their guides to anyone.


************************Step 1: Backups************************

This one is self-explanatory. Just follow your host’s guide to backup your server. For me, I just created a snapshot in Digital Ocean’s web dashboard.

**********************************Step 2: Setup the new server**********************************

I will be writing a whole guide on this process as well. My new server will be running Ubuntu 22.04 since it is an LTS distribution support until well past 2030.

****************Step 3: Taking note of the source server****************

Migrating from one server to another is best done using as similar a target server as possible. Having the same kernel and program versions is preferred, as there will be minimal to no changes in how programs operate on the new machine.

My current server is running on the 5.19.0-46 kernel. The new server runs the 5.15.0-67 kernel. Unfortunately, it is not the same kernel. Fortunately, I don’t have too much on my server to transfer over, so I shouldn’t have any issues with the kernel differences.

While I’m here, I am going to take a look at what I have on the old server and take note of what I need to transfer to the new server. I already know that I am only running Nginx and PM2 to host some Node.js apps, so this is more of a formality than anything. 

I first checked what project files I put on the server. I have a few old projects that I don’t need anymore, but there are three projects that I want transferred over to the new server. All their code is up on Github, but I want to check each project individually to make sure that I hadn’t made any local changes. I can compare the git logs from the old server to the git commits on the respective Github repos. If there are any changes, I will want to make sure that I am copying over the project folder instead of re-downloading and compiling the project from the Github repo. If this were the case, I should also want to look into better repo management. 

I can check to see if I have any commits that are out of sync with the project's Github repo.

`git log` 

I can also check if any individual files were edited and not committed.

`git status`.

Fortunately, I don’t have any inconsistencies between the project files and the repo. 

Next up, I checked the installed programs. I use the apt package manager on my Ubuntu server, so I can get this information through apt’s list of installed apps with the command `apt list --installed`.

As suspected, the only application that isn't part of the traditional distribution is Nginx. But just to make sure, I will also use the command found in the guide to check the services that are available through systemctl. `systemctl list-units -t service`.

There are many other methods of checking what is on the server, including checking systemd targets, checking network processes, and various other lists services, daemons, and service dependencies.

In the end, here is my list of what I found searching through the old server:

********************Old Server********************

OS: Ubuntu 22.10
Kernel: 5.19.0-46-generic

Services:
- Nginx
- Node.js v18.70
- Npm v8.18.0
    - PM2 v-5.2.2

******************Step 4: SSH access between servers******************

I want to be able to access my old server from my new server over SSH. As with any SSH connection, this will involve creating a public key on my new server and adding it the the `autorized_keys` file on my old server. This will give my new server the access required to retrieve files from the old server.

On the new server, I can run the ssh-keygen program and specify using the RSA public-key cryptosystem. This will generate a private and public key pair, which get used to authorize SSH access for our new server.

`ssh-keygen -t rsa` 

Now that we have the public key, we need to put it into the `authorized_keys` file on our old server. The Digital Ocean guide has a super convenient bash script that uses piping to copy the public key from the new server and send it directly to where we want it on the old server.

`cat ~/.ssh/id_rsa.pub | ssh other_server_ip "cat >> ~/.ssh/authorized_keys"`

Unfortunately for me, this command doesn’t work because I have restricted SSH access on my old server to only accept connections from hosts that already have a public key in the old server’s `authorized_keys` file. I will have to manually copy and paste the new server’s public key onto my old server.

Last but not least, I want to check what versions of software I am using. Nginx, Node.js, Npm, and PM2 are the programs that I use on this server. I want to make sure I take note of the Node.js and Npm versions, as those can cause the most issues when running projects.

**********Step 5: Setting up the new server**********

Now that we have a new server running and a list of services we need from our old server, we can begin by installing the services on the new server. This is a simple process of installing each program, so I won’t get into that. Writing a bash script would be great for this purpose, however, I only have four services to install so I am opting to install them manually.

********************************************Step 6: Transferring files********************************************

Now we get to the bulk of what needs to be done, migrating files.

There are many options for transferring files between servers. Protocols for file transfers include HTTPS, FTP, SFTP, SCP, and many more. There is a great tool called rsync that works on the SSH protocol and was specifically built to migrate data between hosts. It uses efficient algorithms to copy only the necessary files. While this is definitely overkill for my use case, it is one of the best options out there for migrating data. An easy alternative would be the SCP program.

SCP differs from rsync by copying files directly without any fancy algorithms. It also uses the SFTP protocol, a confusing trait about SCP that was made by developers who realized the previous SCP/RCP protocol was outdated and unmaintained. Those developers have actually recommended the use of rsync or other programs instead of SCP. This is why I choose to go with rsync.

The reason I said rsync is overkill is because I want to copy my Nginx config files. That’s pretty much it. A couple tiny config files. 

The first file is my nginx sites-enabled file that configures the pathways for my reverse proxy. The following command copies the old server’s config to my new server.

`rsync -a <user>@<old-server-hostname>:/etc/nginx/sites-available/<filename> /etc/nginx/sites-available`

Except I was running into an issue:

![SSH Key Error](/images/blog/dealing-with-eol-ubuntu-server/ssh-key-error.png)

Trying to figure this one out was a confusing process and I still haven’t found the root cause of this issue. It seemingly has to do with SSH trying to use the wrong private key to match with the authorized_keys on the old-sever.

I found a workaround that lets me specify the private key to use when using SSH with rsync.

`sudo rsync -Pav -e "ssh -i $HOME/.ssh/id_rsa" [user@domain](mailto:user@domain):/etc/nginx/sites-available/ryancarr.ca /etc/nginx/sites-available`

There are four flags used in that command that I want to make sure I understand before using the command:

- `-P`  a combination of two other flags
    - `--progress` “show progress during transfer”
    - `--partial`  “keep partially transferred files”
- `-a`  archive. its a combination of `-rlptgoD`
    - `-r` recursive to get all files in a directory
    - `-l` copy all links
    - `-p` keep permissions of files and directories
    - `-t` keep modification times
    - `-g` keep the group of the file or directory
    - `-o` keep the owner of the file or directory
    - `-D` preserves device and special files
- `-v` verbose output
- `-e` lets you specify the remote shell to use

There is a lot to that one command. Honestly, if I wanted to simplify that output for transferring a single file I could run `-Pptgov` instead of `-Pav` but the latter is more concise and universal.

I’m going to repeat this command for the few other files I need. Once completed, the data migration is done.

************************************Step 6: Setup New Server************************************

The migration is done and now we can set up all of our projects, Nginx config files, and anything else we transferred over. 

********************Conclusion********************
As far as my personal needs go, this migration is complete. There is so much more that could be done in terms of migration system users, cron jobs, services, system settings, databases, and much, much more. 

This first migration was a good test for me to experience what is involved in connecting two servers via SSH and moving some basic files between them.
