# HTTP Basic Authentication in Nginx

[Tutorial Link 1](https://www.cloudbooklet.com/http-basic-authentication-nginx-ubuntu-18-04/)

[Tutorial Link 2](https://www.digitalocean.com/community/tutorials/how-to-set-up-password-authentication-with-nginx-on-ubuntu-14-04)

1. Install Apache Tools

   `sudo apt install apache2-utils`

2. Create a password file and add a user

   `sudo htpasswd -c /etc/nginx/.htpasswd sammy`

3) Add the auth layer

   `sudo nano /etc/nginx/sites-available/default`

   And add:

   ```
     location / {
       try_files $uri $uri/ =404;
       auth_basic "Restricted Content";
       auth_basic_user_file /etc/nginx/.htpasswd;
   }
   ```

4) Restart nginx

   `sudo systemctl restart nginx`
