# Assignment 3 Part 1

## Introduction
This repository contains the necessary files and instructions to "setup a Bash script that generates a static index.html file that contains some system information. The script will be configured to run automatically every day at 05:00 using a systemd service and timer. The HTML document created by this script will be served with an nginx web server that will run on your Arch Linux droplet along with a firewall setup using ufw to help secure your server." [1]
### Creating the System User

The first step in this process is creating a system user named Webgen. We want to create this system user, as A system user isolates processes or services from other users and from the root account, reducing security risks and prevents direct access to the system by this user, further increasing security. To create a system user `webgen` with a home directory at `/var/lib/webgen`, a non-login shell, and ownership of its directory and files:

1. create the system user with a non-login shell and home directory 
```bash 
sudo useradd -r -d /var/lib/webgen -s /usr/sbin/nologin webgen
```

-r: creates the system user
-d /var/lib/webgen: specifies the location of the home directory for the new user Webgen
-s /urs/sbin/nologin: specifies the no-login shell to prevent directly logging in with the Webgen user's credentials.

2. Create the home directory for the new user
```bash
sudo mkdir -p /var/lib/webgen  
```

3. Set ownership of the home directory to the user (and subsequent group)
``` 
sudo chown -R webgen:webgen /var/lib/webgen
```

-R: recursively sets the ownership of the file within the specified location to the same ownership as the chown command specifies.
## Creating directories + Moving Necessary Files
Assuming you have already downloaded all the files from this repository, we must now create the file/directory organizational system within the home directory for the script and unit files to work properly:

1. Create necessary directories
```bash
mkdir /var/lib/webgen/bin
mkdir /var/lib/webgen/HTML
```

2. Move `generate_index` script into `bin` folder
```bash
mv generate_index /var/lib/webgen/bin
```

3. Give ownership of subsequent file/directory organizational system to Webgen user and group
```bash
sudo chown -R webgen:webgen /var/lib/webgen
```

4. Change the permissions of the generate_index script to be executable for the user and group
```bash
sudo chmod u,g+x /var/lib/webgen/bin/generate_index
```


## References
[1] McNinch, Nathan. https://learn.bcit.ca/content/enforced/1063362-45842.202430/assignment3p1.pdf
