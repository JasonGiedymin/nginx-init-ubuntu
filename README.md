nginx-init-ubuntu
=================


## Status

[![Build Status](https://travis-ci.org/JasonGiedymin/nginx-init-ubuntu.svg?branch=master)](https://travis-ci.org/JasonGiedymin/nginx-init-ubuntu)

Current release: [v3.9.0](https://github.com/JasonGiedymin/nginx-init-ubuntu/releases/tag/v3.9.0)

Previous stable release [v3.8.0](https://github.com/JasonGiedymin/nginx-init-ubuntu/releases/tag/v3.8.0)

Notes: v3.8.0 has been stable for the last several months without issues. v3.9.0 while
stable, is new.

## Info

Tried and true Nginx init script.

Ubuntu, Vagrant, and [Docker](https://github.com/AnsibleShipyard/ansible-nginx/blob/master/Dockerfile) tested!

You may also want to use the [AnsibleShipyard ansible-nginx playbook](https://github.com/AnsibleShipyard/ansible-nginx).

Simple ansible playbook sits in this repository.

Author: [Jason Giedymin](http://jasongiedymin.com) <jasong -_at_- apache -=dot=- org>

Check out my other [repos](http://github.com/JasonGiedymin)!


## Support

Rest assured that this repo will be maintained _indefinitely_ beyond Ubuntu LTS 
and systemd adoption into Ubuntu stable.


## Last tested with:

1. Ubuntu 14.xx (works with prior versions)
2. [nginx-1.7.9](http://nginx.org/download/nginx-1.7.9.tar.gz) (works with prior versions)


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
    wget http://nginx.org/download/nginx-1.7.9.tar.gz
    tar -xvf nginx-1.7.9.tar.gz
    cd nginx-1.7.9/
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
  - NGINXPATH
  - DAEMON
  - PS
  - PIDNAME
  - PIDFILE
  - PIDSPATH
  - DESCRIPTION
  - RUNAS
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
    
The NGINXPATH value should point to your installation of Nginx, the default is /usr/local/nginx

It's likely you'll need to update the NGINXPATH value if you didn't install from source. Eg, if you install Nginx using apt-get on Ubuntu nginx will be installed to /etc/nginx

    # Changing NGINXPATH when Nginx was installed with apt-get
    NGINXPATH=/etc/nginx


## Testing
Tests run as part of the deployment scripts `integration-tests.yml`.

To start make sure you have [vagrant](http://vagrantup.com), and [ansible](https://github.com/ansible/ansible) installed.

Download the Ubuntu base box:

```bash
vagrant box add ubuntu-14.10 https://cloud-images.ubuntu.com/vagrant/utopic/current/utopic-server-cloudimg-amd64-vagrant-disk1.box
```

Run vagrant:

    vagrant up

Manually provision again:

    vagrant provision

### Using with Docker
A basic Dockerfile will arrive shortly for testing, but note that I focued my efforts on creating an nginx [ansible role](https://github.com/AnsibleShipyard/ansible-nginx). [This repo](https://github.com/AnsibleShipyard/ansible-nginx) has a [Dockerfile](https://github.com/AnsibleShipyard/ansible-nginx/blob/master/Dockerfile) which will install Nginx along with `nginx-init-ubuntu` (this repo) using ansible. Until the basic testing Dockerfile is in place here please refer to the [ansible role](https://github.com/AnsibleShipyard/ansible-nginx) and it's [Dockerfile](https://github.com/AnsibleShipyard/ansible-nginx/blob/master/Dockerfile) -- if your looking for stability.

If your looking for a more production and developer friendly [Dockerfile, look here](https://github.com/AnsibleShipyard/ansible-nginx/blob/master/Dockerfile).

When using the ansible role mentioned above you will need to set `nginx_docker_override` to `True` as the role will detect if running within a Dockerfile. This is to prevent nginx running in `daemon` mode.

A copy of [nginx-init-ubuntu](https://github.com/JasonGiedymin/nginx-init-ubuntu) is present in the [ansible role](https://github.com/AnsibleShipyard/ansible-nginx).

## Contributions ##
_Contributions are welcome!_
