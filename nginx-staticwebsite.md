# How to serve static files using nginx

[Tutorial Link](https://medium.com/@jgefroh/a-guide-to-using-nginx-for-static-websites-d96a9d034940)

1. Create a folder to place your static files

   `cd /var/www && mkdir [websitename]`

2. Configure webpack

   - `cd /etc/nginx/sites-available && sudo nano [serverName]`

   - place this code

   ```server {
    listen 80;
    root /var/www/[websitename];
    index index.html;
    server_name <YourVPSIpAddress>(www.mydomain.ro mydomain.ro);
    location / {
        try_files $uri $uri/ =404;
    }}
   ```
