# Install k9s using Homebrew in Linux (ubuntu)

After installing k9s using snap, it should be noted, this package is not longer mantained so it won't work if you install it.

The potentiall errors, you may receive after running the following:

```
$ k9s
```
```
 ____  __.________       
|    |/ _/   __   \______
|      < \____    /  ___/
|    |  \   /    /\___ \ 
|____|__ \ /____//____  >
        \/            \/ 

Boom!! Unable to connect to api server invalid configuration: [unable to read client-cert /home/ivang/.minikube/profiles/minikube/client.crt for minikube due to open /home/ivang/.minikube/profiles/minikube/client.crt: permission denied, unable to read client-key /home/ivang/.minikube/profiles/minikube/client.key for minikube due to open /home/ivang/.minikube/profiles/minikube/client.key: permission denied, unable to read certificate-authority /home/ivang/.minikube/ca.crt for minikube due to open /home/ivang/.minikube/ca.crt: permission denied].
```
Even certificates are in place as well as permissions to access them, it is impossible to overcome this issue. This broken snap package should be removed from repository but it is not the case as of today 07/08/2022.

Therefore another option to install k9s is using brew according to: https://k9scli.io/topics/install/

The following steps are required to accomplish this:

## Update Ubuntu

```
$ sudo apt-get update
```

```
Hit:1 http://security.ubuntu.com/ubuntu focal-security InRelease
Hit:2 http://us.archive.ubuntu.com/ubuntu focal InRelease                                                               
Hit:3 https://download.docker.com/linux/ubuntu bionic InRelease                                                         
Hit:5 http://us.archive.ubuntu.com/ubuntu focal-updates InRelease   
Hit:6 http://us.archive.ubuntu.com/ubuntu focal-backports InRelease
Hit:4 http://mirrors.edge.kernel.org/ubuntu focal InRelease
Reading package lists... Done
```

## Install Build Essentials
```
$ sudo apt-get install build-essential
```
```
Reading package lists... Done
Building dependency tree       
Reading state information... Done
build-essential is already the newest version (12.8ubuntu1.1).
The following packages were automatically installed and are no longer required:
  libbsd0:i386 libedit2:i386 libstdc++6:i386 libtinfo5:i386 python-certifi python-cffi-backend python-cryptography python-enum34 python-idna python-ipaddress
  python-openssl python-tz python3.7-distutils python3.7-lib2to3
Use 'sudo apt autoremove' to remove them.
0 to upgrade, 0 to newly install, 0 to remove and 0 not to upgrade.
```

## Install Git
```
$ sudo apt install git -y
```

## Run Homebrew installation script
```
$ /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```
```
==> Checking for `sudo` access (which may request your password)...
==> Select a Homebrew installation directory:
- Enter your password to install to /home/linuxbrew/.linuxbrew (recommended)
- Press Control-D to install to /home/ivang/.linuxbrew
- Press Control-C to cancel installation
[sudo] password for ivang: 
==> This script will install:
...
==> Next steps:
- Run these two commands in your terminal to add Homebrew to your PATH:
    echo 'eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)"' >> /home/ivang/.zprofile
    eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)"
- Install Homebrew's dependencies if you have sudo access:
    sudo apt-get install build-essential
  For more information, see:
    https://docs.brew.sh/Homebrew-on-Linux
- We recommend that you install GCC:
    brew install gcc
- Run brew help to get started
- Further documentation:
    https://docs.brew.sh
```

Following the recommendations after installing Homebrew:

#### Add Homebrew to system path (instead .zprofile it could be .zshrc or .bashrc)
```
echo 'eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)"' >> /home/ivang/.zprofile
```

```
$ eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)"   
```

#### Additionally check Hombrew $PATH
```
$ echo $PATH
```
```
/home/linuxbrew/.linuxbrew/bin:/home/linuxbrew/.linuxbrew/sbin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin
```

#### Content of .zprofile file
```
$ cat .zprofile                                                                                                                                      ✔ 
```
```
eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)"
```


#### Checking Homebrew version
```
$ brew -v 
```
```
Homebrew 3.5.8
Homebrew/homebrew-core (git revision 3d2972b437c; last commit 2022-08-07)
```

#### Install GCC as pointed out by installation output
```
$ brew install gcc
```
```
Running `brew update --auto-update`...
==> Downloading https://
...
==> Installing gcc
==> Pouring gcc--12.1.0.x86_64_linux.bottle.tar.gz
...
==> Running `brew cleanup gcc`...
```

#### Making sure Homebrew is ready

```
$ brew doctor                                                                                                                             ✔  3m 43s  
```
```
Your system is ready to brew.
```

## Homebrew Uninstallation Script (in case you want to revert back changes)
```
$ /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/uninstall.sh)"
```

## Finally in order to Install k9s
```
$ brew install derailed/k9s/k9s                                                                                                              ✔  46s  
```
```
Running `brew update --auto-update`...
==> Tapping derailed/k9s
Cloning into '/home/linuxbrew/.linuxbrew/Homebrew/Library/Taps/derailed/homebrew-k9s'...
remote: Enumerating objects: 816, done.
remote: Counting objects: 100% (400/400), done.
...
==> Installing k9s from derailed/k9s
🍺  /home/linuxbrew/.linuxbrew/Cellar/k9s/0.26.3: 5 files, 53.3MB, built in 16 seconds
````

## Checking k9s installation

In this case, there is a minikube installation running.

first make sure docker is running:
```
$ sudo service docker status
```

otherwise, start/restart docker:
```
$ sudo service docker restart
```

then, start minikube:
```
$ minikube start 
```

check minikube status,
```
$ minikube status                                                                                                                                    ✔ 
```
```
minikube
type: Control Plane
host: Running
kubelet: Running
apiserver: Running
kubeconfig: Configured
```

Additionally, the config file is in the home directory under .kube folder:
```
$ ls -la
```
```
drwxr-xr-x  4 ivang docker   4096 Aug  7 19:55  .kube
```

Furthermore

```
 $ ~/.kube> ls -la                                                                                                                                       ✔ 
```
```
drwxr-x---  4 ivang docker 4096 Dec 16  2021 cache
-rw-------  1 ivang docker  824 Aug  7 16:44 config
```

### Double cheking k9s is working
```
$ k9s
```
&nbsp;
<p align="center">
<img width="800" height="250" src="https://user-images.githubusercontent.com/67383481/183307035-46e9831f-a03f-4dec-b62f-fc84e1542f3d.png">
</p>
&nbsp;

### k9s installation info
```
 $ k9s info 
 ```
 ```
 _  _  __.________       
|    |/ _/   __   \______
|      < \____    /  ___/
|    |  \   /    /\___ \ 
|____|__ \ /____//____  >
        \/            \/ 

Configuration:   /home/ivang/.config/k9s/config.yml
Logs:            /tmp/k9s-ivang.log
Screen Dumps:    /tmp/k9s-screens-ivang
```



**Note:
For further k9s tuning go to:

https://github.com/IvanGDR/Installing-K9S-in-macOS-and-connecting-to-Remote-K8S-cluster/blob/main/README.md

I used brew to install kubectx+kubens+popeye
for kubectl in my case I got it already installed using apt-get package manager.
