# nginx-init-ubuntu #

Tried and true Nginx init script.

Author: [Jason Giedymin](http://jasongiedymin.com) <jasong -_at_- apache -=dot=- org>

Check out my other [repos](http://github.com/JasonGiedymin)!


## Last tested with:

1. Ubuntu 12.10
2. [nginx-1.3.16](http://nginx.org/download/nginx-1.3.16.tar.gz)


## Notes ##
It is recommended to install [Nginx](http://nginx.net/) by doing a full compile & build. Not all package repositories keep their branches updated. For security it is your duty to maintain a good working environment and thus includes all interfacing applications.
This script works turn-key with the default compile of nginx. It is fully recommended that you go through the variables contained within this script if you have a custom compiled build.

A great resource is the [Nginx Wiki](http://wiki.nginx.org/).


## Basic Install ##
Basic install instructions, use sudo if necessary for the below (depends on your setup/security).

    # [optional as you may have these installed]
    sudo apt-get install libpcre3-dev zlib1g-dev
    
    mkdir ~/temp/nginx-install
    cd ~/temp/nginx-install
    
    # download/curl/wget nginx 
    wget http://nginx.org/download/nginx-1.3.16.tar.gz
    tar -xvf nginx-1.3.16.tar.gz
    cd nginx-1.3.16/
    ./configure
    make
    sudo make install
    
    #copy/download/curl/wget the init script
    sudo wget https://raw.github.com/JasonGiedymin/nginx-init-ubuntu/master/nginx -O /etc/init.d/nginx
    sudo chmod +x /etc/init.d/nginx
    
    service nginx status  # to poll for current status
    service nginx stop    # to stop any servers if any
    service nginx start   # to start the server
    
    #[optional] 
    sudo update-rc.d -f nginx defaults

    #[optional remove the upstart script]
    sudo update-rc.d -f nginx remove

## Contributions ##
_Contributions are welcome!_
