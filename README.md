# Install-Homebrew-in-Linux-ubuntu


## Update Ubuntu
'''
$ sudo apt-get update
'''

Hit:1 http://security.ubuntu.com/ubuntu focal-security InRelease
Hit:2 http://us.archive.ubuntu.com/ubuntu focal InRelease                                                               
Hit:3 https://download.docker.com/linux/ubuntu bionic InRelease                                                         
Hit:5 http://us.archive.ubuntu.com/ubuntu focal-updates InRelease   
Hit:6 http://us.archive.ubuntu.com/ubuntu focal-backports InRelease
Hit:4 http://mirrors.edge.kernel.org/ubuntu focal InRelease
Reading package lists... Done


Install Build Essentials
$ sudo apt-get install build-essential

Reading package lists... Done
Building dependency tree       
Reading state information... Done
build-essential is already the newest version (12.8ubuntu1.1).
The following packages were automatically installed and are no longer required:
  libbsd0:i386 libedit2:i386 libstdc++6:i386 libtinfo5:i386 python-certifi python-cffi-backend python-cryptography python-enum34 python-idna python-ipaddress
  python-openssl python-tz python3.7-distutils python3.7-lib2to3
Use 'sudo apt autoremove' to remove them.
0 to upgrade, 0 to newly install, 0 to remove and 0 not to upgrade.


Install Git

$ sudo apt install git -y




Run Homebrew installation script

$ /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

==> Checking for `sudo` access (which may request your password)...
==> Select a Homebrew installation directory:
- Enter your password to install to /home/linuxbrew/.linuxbrew (recommended)
- Press Control-D to install to /home/ivang/.linuxbrew
- Press Control-C to cancel installation
[sudo] password for ivang: 
==> This script will install:


