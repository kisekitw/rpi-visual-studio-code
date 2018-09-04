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

### 3. MQTTS broker - Mosca && pino-pretty

1. Open a new command prompt/terminal, Then run the following:

~~~npm
npm install mosca pino-pretty -g
~~~

2. Check whether openssl is present on machine, run **openssl version -a** and you should see the information about local installation of openssl.

3. Create a new folder named **broker**, inside the **broker** folder, create another folder named **certs** and **cd** into that folder. 

4. Run the following to generate the required key and certificate file, this will prompt a few questions and you can fill in the same along the following lines:

~~~npm 
openssl req -newkey rsa:2048 -nodes -keyout key.pem -x509 -days 365 -out certificate.pem
~~~

5. This will create two new files inside the certs folder named **key.pem** and **certificate.pem**

6. At the root of the **broker** folder, create a new file named **index.js** and update it as follows:

~~~index.js
let SSL_KEY = __dirname + '/certs/key.pem';
let SSL_CERT = __dirname + '/certs/certificate.pem';
let MONGOURL = 'mongodb://admin:admin123@ds241055.mlab.com:41055/iotfwjs';

module.exports = {
    id: 'broker',
    stats: false,
    port: 8443,
    logger: {
        name: 'iotfwjs',
        level: 'debug'
    },
    secure: {
        keyPath: SSL_KEY,
        certPath: SSL_CERT,
    },
    backend: {
        type: 'mongodb',
        url: MONGOURL
    },
    persistence: {
        factory: 'mongo',
        url: MONGOURL
    }
};
~~~

7. Save **index.js** and head back to the terminal/prompt and **cd** into the location where we have the **index.js** file. Next, run the following:

~~~npm 
mosca -c index.js -v | pino-pretty
~~~

ref. http://mcollina.github.io/ascoltatori/#brokers

