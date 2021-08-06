# F.A.Q.

## Where is the SQL File?
FSN on first launch as long as everything is connected properly and installed properly will AUTOMATICALLY create all the tables and columns you need in your database. On first run your server console will show the tables being made. It is recommened that after the first run you close the server and restart it. Just to make sure the tables have been created and you are connected to your database.


## Stuck at the character Select Screen/ Black Screen on connection?
Make sure your database is properly setup and connected in your server.cfg. You need the mysql string at the top of the file and you need to point it to the correct mysql server with the correct username and password. This error is majority of the time showing as your database is not properly configured. 

Example of a mysql string `set mysql_connection_string "server=localhost;userid=root;password=mysecretpassword;database=fsn"` 

If you are hosting your database on a seperate server be sure to change the server=localhost to match your database server ip address. Also make sure you are using the correct version of mysql-async from the readme/installation page.

## I can't buy a car help!
You probably did not install mythic_notify. Check your client console logs and try again after installing mythic_notify.

## Why can't I get a phone number at the store?
You probably changed the folder structure of the resources and how they are installed. The phone script needs to point to the correct folder in order to save texts, contacts, etc to a datastore folder. If you installed your resources like so /resources/[fsn]/allyourfsnresources then you will need to change [line](https://github.com/jamessc0tt/FiveM-FSN-Framework/blob/master/fsn_phones/sv_phone.lua#L2)

From
` 'resources/'..GetCurrentResourceName()..'/datastore/' `

To
` 'resources/[fsn]/'..GetCurrentResourceName()..'/datastore/' `

 You will also need to do this for the evidence locker on this [line](https://github.com/JamesSc0tt/FiveM-FSN-Framework/blob/master/fsn_inventory/pd_locker/sv_locker.lua#L2)

# Known Bugs/Issues
You can check the latest issues and bugs on the github under [issues](https://github.com/JamesSc0tt/FiveM-FSN-Framework/issues) This list MAY NOT be up to date with the latest issues and bugs

..* Clothing menu breaks on texture change

..* Facial features do not save