# F.A.Q.

## Where is the SQL File?
FSN on first launch as long as everything is connected properly and installed properly will AUTOMATICALLY create all the tables and columns you need in your database. On first run your server console will show the tables being made. It is recommened that after the first run you close the server and restart it. Just to make sure the tables have been created and you are connected to your database.


## Stuck at the character Select Screen/ Black Screen on connection?
Make sure your database is properly setup and connected in your server.cfg. You need the mysql string at the top of the file and you need to point it to the correct mysql server with the correct username and password. This error is majority of the time showing as your database is not properly configured. Example of a mysql string `set mysql_connection_string "server=localhost;userid=root;password=mysecretpassword;database=fsn"` If you are hosting your database on a seperate server be sure to change the server=localhost to match your database server ip address.


# Known Bugs/Issues
You can check the latest issues and bugs on the github under [issues](https://github.com/JamesSc0tt/FiveM-FSN-Framework/issues) This list MAY NOT be up to date with the latest issues and bugs
..* Clothing menu breaks on texture change
..* Facial features do not save