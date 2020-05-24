# Some useful commands for mongo.

1. Check status

   `sudo cat /var/log/mongodb/mongod.log`

2) Start shell

   `mongo`

3) Check version

   `mongod --version`

4. Create new database

   `use new_database` - create new database

   `db` - check the currently selected db

   `db.new_collection.insert({ some_key: "some_value" })` - u can't create an empty db so you have to insert a collection and some data

   `show dbs` - check if the db was created

   `db.createUser({ user: "new_user", pwd: "some_password", roles: [ { role: "readWrite", db: "new_database" }]})` - create a new user with read/write permissions

5) Connect to a database with credentials

`mongo -u db_user -p db_pwd db_name`

6. Create a dump file of a database

`mongodump --host="127.0.0.1:27017" -u [db_user] -p [db_pwd] -d [db_name] -o [output_path]`

7. Create db from a dump file

`mongorestore -u [auth-user] -p [auth-user-pwd] --authenticationDatabase [admin-db-name] -d [new-db-name] [path-to-dump-folder]`

8. Print current user

`db.runCommand({connectionStatus: 1})`

9. Prin collections

`db.runCommand( { listCollections: 1.0, nameOnly: true } )`

10. Update user with restore backup db roles (only working for admin db)

- connect to database with auth
- select the database
- `db.updateUser("AdminGeorgian",{roles:[{role:"restore",db:"admin"},{role:"backup",db:"admin"},{ role: "userAdminAnyDatabase", db: "admin" }]});`

11. Delete user

`use [db_name]`
`db.dropUser("[user-name]")`

12. Drop collection
    db.[collection].drop();
