# How to secure mongodb

1. Add an admin user

   ```
   use admin
   db.createUser(
   {
     user: "AdminSammy",
     pwd: "AdminSammy'sSecurePassword",
     roles: [ { role: "userAdminAnyDatabase", db: "admin" } ]
   }
   )
   ```

2. Enabling Authentication

   `sudo nano /etc/mongod.conf`

   In the **#security** section, we’ll remove the hash in front of security to enable the stanza. Then we’ll add the authorization setting. When we’re done, the lines should look like the excerpt below:

   ```
     security: -> no white space
       authorization: "enabled"  -> 2 white spaces
   ```

3) Restart the daemon

   `sudo systemctl restart mongod`

4) CHeck the status

   `sudo systemctl status mongod`

   Watch for `Active: active (running)` in the output

5. Verifying that Unauthenticated Users are Restricted

   `mongo`

   `use admin`

   `db.getUsers()`

   The access should be restricted.

6. Verifying the Administrative User’s Access

   `mongo -u AdminGeorgian -p --authenticationDatabase admin`
