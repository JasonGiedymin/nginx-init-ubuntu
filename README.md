# nginx-init-ubuntu #

Tried and true Nginx init script.

Author: [Jason Giedymin](http://jasongiedymin.com) <jasong -_at_- apache -=dot=- org>

Check out my other [repos](http://github.com/JasonGiedymin)!


## Last tested with:
1. Ubuntu 12.10
2. [nginx-1.3.16](http://nginx.org/download/nginx-1.3.16.tar.gz)


## Notes ##
It is recommended to install [Nginx](http://nginx.net/) by doing a full compile & build. Not all package repositories keep their branches updated. For security it is your duty to maintain a good working environment and thus includes all interfacing applications.
This script works turn-key with the default compile of ngin. It is fully recommended that you go through the variables contained within this script if you have a custom compiled nginx install.

A great resource is the [Nginx Wiki](http://wiki.nginx.org/).


## Basic Install ##
Basic install instructions, use sudo if necessary for the below (depends on your setup/security).
1. [optional as you may have these installed] sudo apt-get install libpcre3-dev zlib1g-dev
2. download/curl/wget nginx 
2. tar -xvf <nginx.ver.tar>
3. cd nginx-<dot-version>
4. ./configure
5. make
6. sudo make install
7. copy/download/curl/wget the init script
8. chmod +x nginx
9. ./nginx status
10. ./nginx start
11. ./nginx stop
12. [optional] sudo update-rc.d -f nginx defaults


## Contributions ##
_Contributions are welcome!_
