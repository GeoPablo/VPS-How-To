# How connect to your github account using SSH (read/write)

1. Configure Git

   `git config --global user.name "Your User Name"`

   `git config --global user.email "example@example.com"`

2. Check your configuration

   `git config --list`

3. Generate a SSH key for Github(if you don't already have one)

   `ssh-keygen -t rsa -b 4096 -C "example@example.com"`

4. Copy the public key to github

   `cd ~/.ssh && cat id_rsa.pub`
