# How to run a NodeJS app on VPS

1. Start the app with pm2

   - `sudo npm i -g pm2` - install pm2 as process manager

   - `pm2 start [mainfile.js]` - run the main file

2. Make the app start on boot

   - `pm2 startup` - this will print a command to run after you started your app

   - `pm2 save` - save the process (save the current processes to start them on bootup)

3. Add a domain
   Now you can find the app at http://[yourdomain]:[appPort]

4. Add a reverse proxy to map your app

   - `sudo apt-get install nginx` - install nginx

   - `cd /etc/nginx/sites-available && sudo nano [serverName]`

   - place this code

   ```server {
    listen 80;
    server_name <YourVPSIpAddress>(www.mydomain.ro mydomain.ro);
    location / {
        proxy_pass http://localhost:3000/;
    }}
   ```

   - `sudo nginx -t` - check if your configuration is ok; should see this

   ```
   nginx: the configuration file /etc/nginx/nginx.conf syntax is ok

   nginx: configuration file /etc/nginx/nginx.conf test is successful
   ```

   - `sudo ln -s /etc/nginx/sites-available/[serverName] /etc/nginx/sites-enabled` - enable your configuration; make a symbolic link

   - `sudo systemctl restart nginx` - restart nginx

5) HTTP -> HTTPS

   [Cerbot for ubuntu and nginx](https://certbot.eff.org/lets-encrypt/ubuntubionic-nginx)

6) Disabling startup system from pm2 (**optional**)

   - `pm2 delete [appCode]`
   - `pm2 cleardump`
   - `pm2 save`

   **!** To restart the app again just run it and save the changes in pm2:
   `pm2 start [mainFile] && pm2 save`
