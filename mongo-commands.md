# Some useful commands for mongo.

1. Check status

   `sudo cat /var/log/mongodb/mongod.log`

2) Start shell

   `mongo`

3) CHeck version

   `mongod --version`

4. Create new database

   `use new_database` - create new database

   `db` - check the currently selected db

   `db.new_collection.insert({ some_key: "some_value" })` - u can't create an empty db so you have to insert a collection and some data

   `show dbs` - check if the db was created

   `db.createUser( { user: "new_user", pwd: "some_password", roles: [ { role: "readWrite", db: "new_database" } ] } )` - create a new user with read/write permissions
