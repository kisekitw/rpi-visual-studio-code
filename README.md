# rpi-visual-studio-code
## Installation Guide

### Install Visual Studio Code

~~~Command Line Script
sudo -s
. <( wget -O - https://code.headmelted.com/installers/apt.sh )
~~~

ref: https://edwardkuo.imas.tw/paper/2018/04/14/VisualStudio/RaspberryPiVScode/


### Install MongoDB

~~~Command Line Script
$ sudo apt-get update
$ sudo apt-get upgrade
$ sudo apt-get install mongodb-server

$ sudo service mongod start

$ mongo
~~~

