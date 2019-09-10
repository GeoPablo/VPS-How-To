# Setup for vps

1. Setup SSH keys with PuttyGen (private and public)
2. Create new user and authorize

   `adduser [username]` - add user

   `usermod -aG sudo [username]` - set it as superuser

   `sudo su - [username]` - login as that user

3. Authorize the key for new user

   `mkdir ~/.ssh` - create an ssh dir in hom dir

   `chmod 700 ~/.ssh` - protect the file against any access from other users

   `nano ~/.ssh/authorized_keys` - create a file for the authorized ssh keys and paste your public key;
   add **ssh-rsa** in front of the key and make sure is on a single line not multiple lines( no white space)

   `chmod 600 ~/.ssh/authorized_keys` - set it as a private file only changeable by the user who entered this command.

   `sudo service ssh restart` - restart the ssh service

4. Disable Root & Password Login

   `sudo nano /etc/ssh/sshd_config` - edit this file;

   1. Set **PermitRootLogin** to **no**
   2. Set **PasswordAuthentication** to **no**

   `sudo systemctl reload sshd` - reload sshd

5. Update if you want

   `sudo apt-get update`

6. Firewall

[Firewall Ubuntu 18](https://hostadvice.com/how-to/how-to-configure-firewall-with-ufw-on-ubuntu-18/)
