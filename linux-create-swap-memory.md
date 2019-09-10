# How to create swap memory for linux

1. If there's enough available space, you can create a swap file. For example, we create a 1 GB swap file.

   `sudo fallocate -l 1G /swapfile`

2) Verify the amount of swap file that just created.

   `ls -lh /swapfile`

3) Next, enable the swap file. But first, make /swapfile accessible to "root".

   `sudo chmod 600 /swapfile`

4) Check permission changes.

   `ls -lh /swapfile`

   You should see permission like this:
   `-rw------- 1 root root 1.0G Jan 23 01:44 /swapfile`

5) Next, mark the swap space by this command.

   `sudo mkswap /swapfile`

6) Next, make enable the swap file.

   `sudo swapon /swapfile`

7) Verify available swap.

   `sudo swapon --show`

8) Check again swap space by this command.

   `free -h`

9) To make swap permanent, add this file information to "/etc/fstab".

   `echo '/swapfile none swap sw 0 0' | sudo tee -a /etc/fstab`
