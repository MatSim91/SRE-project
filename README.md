<h1 align="center">SRE project</h1>

**Overview:** Project implementation of SRE practices

# Table Of Contents

1. [Machine Specs](#machine-specs)
2. [Setting up SSH connection to the VM](#setting-up-ssh-connection-to-the-vm)
    - [Windows](#windows)
    - [Linux](#linux)
3. [Creating User](#creating-user)




# Machine Specs

Created a Compute Instance on cloud.oracle.com using the Free Tier account.

**Machine Specs:**

```
VM.Standard.E2.1.Micro
Network bandwidth (Gbps): 0.48
1 OCPU
2.0 GHz AMD EPYC™ 7551 (Naples)
1GB of Memory
46.6 GB of Boot Volume
```

**OS image:**
```
Canonical Ubuntu 24.04
```

# Setting up SSH connection to the VM

## Windows

1. Generate an SSH key pair and save the private and the public key on your local windows machine.
2. Open command prompt and run `ssh-keygen -t rsa` to create local files.
3. Go to your recently created .ssh config that should be on path `C:\Users\<YourUsername>\.ssh\`
   
```
14/03/2025  17:01             2,602 id_rsa
14/03/2025  17:01               567 id_rsa.pub
```

5. Open your private (id_rsa) on a notepad with `notepad id_rsa` and replace the contents with the VM private key you have generated and downloaded in step 1.
6. Open your public key (id_rsa.pub) on a notepad with and `notepad id_rsa.pub` and replace the text content with the VM public key you have generated and downloaded in step 1.
7. Copy your VM public address and SSH into the server with: `ssh -i C:\Users\<YOUR_USERNAME>\.ssh\id_rsa ubuntu@<SERVER_PUBLIC_IP_ADDRESS>`

# Creating User

To stop using root every time I was connected to the serve,r I have created a username by running `sudo adduser mateus`

Then to add my user to the sudo group I ran `sudo usermod -aG sudo mateus`

And we can check that was successful by running `groups mateus`:

```
/home# groups mateus
mateus : mateus sudo
```
## Setting up SSH connection for new User

1. Switch to the new user with `sudo su - mateus`
2. Create the `.ssh` directory in the home folder for the user with
```
mkdir -p ~/.ssh
chmod 700 ~/.ssh
```
3. Create the `authorized_keys` file `nano ~/.ssh/authorized_keys`
4. Copy the public key (from C:\Users\<YOUR_USERNAME>\.ssh\id_rsa.pub on your Windows machine) into the `authorized_keys` file
5. Save the file and set the correct permissions with `chmod 600 ~/.ssh/authorized_keys`
6. Exit the server and attempt SSH connection with `ssh -i C:\Users\<USERNAME>\.ssh\id_rsa <USERNAME>@<SERVER_IP>`

## Linux
