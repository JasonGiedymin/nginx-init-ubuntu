# nginx-init-ubuntu #

Tried and true Nginx init script.

Author: [Jason Giedymin](http://jasongiedymin.com) <jasong -_at_- apache -=dot=- org>

Check out my other [repos](http://github.com/JasonGiedymin)!


## Support

Rest assured that this repo will be maintained _indefinitely_ beyond Ubuntu LTS 
and systemd adoption into Ubuntu stable.


## Last tested with:

1. Ubuntu 12.xx & 13.xx
2. [nginx-1.5.9](http://nginx.org/download/nginx-1.5.9.tar.gz) - should also work with 1.6.xx series, just haven't tested it yet.


## Notes ##
It is recommended to install [Nginx](http://nginx.net/) by doing a full compile & build. Not all package repositories keep their branches updated. For security it is your duty to maintain a good working environment and thus includes all interfacing applications.
This script works turn-key with the default compile of nginx. It is fully recommended that you go through the variables contained within this script if you have a custom compiled build.

A great resource is the [Nginx Wiki](http://wiki.nginx.org/).


## Basic Install ##
Basic install instructions, use sudo if necessary for the below (depends on your setup/security).

    # [optional as you may have these installed]
    sudo apt-get install libpcre3-dev zlib1g-dev
    
    mkdir -p ~/temp/nginx-install
    cd ~/temp/nginx-install
    
    # download/curl/wget nginx 
    wget http://nginx.org/download/nginx-1.5.9.tar.gz
    tar -xvf nginx-1.5.9.tar.gz
    cd nginx-1.5.9/
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


## Advanced Configuration ##
If you need to override the values within the script you should use `/etc/default/nginx`.

You can override any of these values:

  - PATH
  - DAEMON
  - PS
  - PIDNAME
  - PIDFILE
  - PIDSPATH
  - DESCRIPTION
  - RUNAS
  - lockfile
  - NGINX_CONF_FILE


For instance, if you needed to change the description of the server during logging:

    # Edit [/etc/default/nginx] and add the below line
    DESCRIPTION="My Awesome Nginx Server..."

    # Next run the below command:
    sudo service nginx restart

    # Output of running restart with nginx defaults file:
    * Stopping My Super Nginx Server...                                  [ OK ] 
    * Starting My Super Nginx Server...                                  [ OK ]

    # Notice that is says "My Super Nginx Server..." as opposed to the default
    # "Nginx Server...".


## Testing
Tests run as part of the deployment scripts `integration-tests.yml`.

To start make sure you have [vagrant](http://vagrantup.com), and [ansible](https://github.com/ansible/ansible) installed.

Download the Ubuntu base box:

    vagrant box add
    # http://cloud-images.ubuntu.com/vagrant/saucy/current/saucy-server-cloudimg-amd64-vagrant-disk1.box

Run vagrant:

    vagrant up

Manually provision again:

    vagrant provision


## Contributions ##
_Contributions are welcome!_
