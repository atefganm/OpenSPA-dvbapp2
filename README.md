## Our buildserver is currently running on: ##

> Ubuntu 20.04.2 LTS (Kernel 5.4.0) 64 Bit Server OS

## minimum hardware requirement : ##

> RAM:  16GB
> 
> SWAP: 8GB
> 
> CPU:  Multi core\thread Model
> 
> HDD:  for Single Build 250GB Free, for Multibuild 500GB or more

## openSPA 8.0 is build using oe-alliance build-environment and several git repositories: ##

> [https://github.com/oe-alliance/oe-alliance-core/tree/5.0](https://github.com/oe-alliance/oe-alliance-core/tree/5.0 "OE-Alliance")
> 
> [https://github.com/openspa/dvbapp2/tree/8.0](https://github.com/openspa/dvbapp2/tree/8.0 "openSPA E2")
> 
> [https://github.com/openspa/MetrixHD](https://github.com/openspa/MetrixHD/tree/dev "openSPA Skin")

> and a lot more...


----------

# Building Instructions #

1 - Install packages on your buildserver

    sudo apt-get install -y autoconf automake bison bzip2 chrpath coreutils cpio curl cvs debianutils default-jre default-jre-headless diffstat flex g++ gawk gcc gcc-8 gcc-multilib g++-multilib gettext git git-core gzip help2man info iputils-ping java-common libc6-dev libegl1-mesa libglib2.0-dev libncurses5-dev libperl4-corelibs-perl libproc-processtable-perl libsdl1.2-dev libserf-dev libtool libxml2-utils make ncurses-bin patch perl pkg-config psmisc python3 python3-git python3-jinja2 python3-pexpect python3-pip python-setuptools qemu quilt socat sshpass subversion tar texi2html texinfo unzip wget xsltproc xterm xz-utils zip zlib1g-dev libuchardet-dev uchardet
    
----------
2 - Set python3 as preferred provider for python

    sudo update-alternatives --install /usr/bin/python python /usr/bin/python2 1
    sudo update-alternatives --install /usr/bin/python python /usr/bin/python3 2
    sudo update-alternatives --config python
    select python3
    
----------    
3 - Set your shell to /bin/bash.

    sudo dpkg-reconfigure dash
    When asked: Install dash as /bin/sh?
    select "NO"

----------
4 - modify max_user_watches

    echo fs.inotify.max_user_watches=524288 | sudo tee -a /etc/sysctl.conf

    sudo sysctl -n -w fs.inotify.max_user_watches=524288

----------
5 - Add user openspabuilder

    sudo adduser openspabuilder

----------
6 - Switch to user openspabuilder

    su openspabuilder

----------
7 - Switch to home of openspabuilder

    cd ~

----------
8 - Create folder openspa8.0

    mkdir -p ~/openspa8.0

----------
9 - Switch to folder openspa8.0

    cd openspa8.0

----------
10 - Clone oe-alliance git

    git clone git://github.com/oe-alliance/build-enviroment.git -b 5.0

----------
11 - Switch to folder build-enviroment

    cd build-enviroment

----------
12 - Update build-enviroment

    make update

----------
13 - Finally you can start building a image

    MACHINE=zgemmah9combo DISTRO=openspa DISTRO_TYPE=release make image

