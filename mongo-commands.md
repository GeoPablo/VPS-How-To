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

# DB migration

[article](https://softwareontheroad.com/database-migration-node-mongo/)

1. `npm i migrate-mongo`
2. `npx migrate-mongo init`

_migrate-mongo-config.js_

```js
// In this file you can configure migrate-mongo
const { parse } = require("dotenv");
const { readFileSync } = require("fs");
const env = parse(readFileSync(`./.env.${process.env.NODE_ENV}`));

const config = {
  mongodb: {
    url: env.MONGODB_URI,

    // TODO Change this to your database name:
    // databaseName: env.mongo.dbname,

    options: {
      useNewUrlParser: true, // removes a deprecation warning when connecting
      useUnifiedTopology: true, // removes a deprecating warning when connecting
      //   connectTimeoutMS: 3600000, // increase connection timeout to 1 hour
      //   socketTimeoutMS: 3600000, // increase socket timeout to 1 hour
    },
  },

  // The migrations dir, can be an relative or absolute path. Only edit this when really necessary.
  migrationsDir: "migrations",

  // The mongodb collection where the applied changes are stored. Only edit this when really necessary.
  changelogCollectionName: "changelog",

  // The file extension to create migrations and search for in migration dir
  migrationFileExtension: ".js",
};

// Return the config as a promise
module.exports = config;
```

3. `npx migrate-mongo create my-migration`

4. Add `"migrate:dev:up": "cross-env NODE_ENV=development migrate-mongo up"` inside `package.json` scripts

5. Run `npm run migrate:dev:up`

This will run all the `up` functions and it will create a collection named `changelog` to know what migrations were runned and what it should run next.
