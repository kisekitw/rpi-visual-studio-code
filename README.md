# rpi-visual-studio-code
## Installation Guide

### 1. Install Visual Studio Code

~~~Command Line Script
sudo -s
. <( wget -O - https://code.headmelted.com/installers/apt.sh )
~~~

ref: https://edwardkuo.imas.tw/paper/2018/04/14/VisualStudio/RaspberryPiVScode/


### 2. Install MongoDB

~~~Command Line Script
$ sudo apt-get update
$ sudo apt-get upgrade
$ sudo apt-get install mongodb-server

$ sudo service mongod start

$ mongo
~~~

ref: http://yannickloriot.com/2016/04/install-mongodb-and-node-js-on-a-raspberry-pi/

It would install MongoDB shell version: 2.4.14
To add admin, need use old API:

~~~Mongo API
use <dbname>

db.addUser( { user: "<username>",pwd: "<password>",roles: [ "userAdminAnyDatabase" | "userAdmin"] } )

db.auth("youruser", "yourpassword") //return 1 means login success

show collections
~~~

ref: https://github.com/andresvidal/rpi3-mongodb3
ref: https://docs.mongodb.com/v2.4/tutorial/add-user-administrator/

### 3. Mosca



ref. http://mcollina.github.io/ascoltatori/#brokers

