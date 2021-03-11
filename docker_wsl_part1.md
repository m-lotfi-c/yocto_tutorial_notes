# Install from a package
- If you cannot use Docker’s repository to install Docker Engine, 
- you can download the .deb file for your release and install it manually. 
- You need to download a new file each time you want to upgrade Docker.
- Go to https://download.docker.com/linux/ubuntu/dists/, 
- choose your Ubuntu version, 
- then browse to pool/stable/, 
- choose amd64, armhf, or arm64, and 
- download the .deb file for the Docker Engine version you want to install.

Install Docker Engine, changing the path below to the path where you downloaded the Docker package.
```
    $ sudo dpkg -i /path/to/package.deb
```


# Install using the repository
- Before you install Docker Engine for the first time on a new host machine, 
- you need to set up the Docker repository. 
- Afterward, you can install and update Docker from the repository.

SET UP THE REPOSITORY
- Update the apt package index and install packages to allow apt to use a repository over HTTPS:
```
    $ sudo apt-get update
    $ sudo apt-get install apt-transport-https ca-certificates curl gnupg lsb-release
```
Add Docker’s official GPG key:
```
    $ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```

- Use the following command to set up the stable repository. 
- To add the nightly or test repository, add the word nightly or test (or both) after the word stable in the commands below. 
- Learn about nightly and test channels.

- Note: 
- The lsb_release -cs sub-command below returns the name of your Ubuntu distribution, such as xenial. 
- Sometimes, in a distribution like Linux Mint, you might need to change $(lsb_release -cs) to your parent Ubuntu distribution. 
- For example, if you are using Linux Mint Tessa, you could use bionic. 
- Docker does not offer any guarantees on untested and unsupported Ubuntu distributions.
- x86_64 / amd64

```
echo \
  "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

INSTALL DOCKER ENGINE
- Update the apt package index, and install the latest version of Docker Engine and containerd, or 
- go to the next step to install a specific version:
- go to /etc/apt/sources.list and uncoment deb-src then 
``` 
    $ sudo nano /etc/apt/sources.list
    $ sudo apt-get update
    $ sudo apt-get install docker-ce docker-ce-cli containerd.io
```

Got multiple Docker repositories?
- If you have multiple Docker repositories enabled, 
- installing or updating without specifying a version in the apt-get install or 
- apt-get update command always installs the highest possible version, 
- which may not be appropriate for your stability needs.

To install a specific version of Docker Engine, list the available versions in the repo, then select and install:
a. List the versions available in your repo:
```
    $ apt-cache madison docker-ce
```
output 
```
 docker-ce | 5:20.10.5~3-0~ubuntu-bionic | https://download.docker.com/linux/ubuntu bionic/stable amd64 Packages
 docker-ce | 5:20.10.4~3-0~ubuntu-bionic | https://download.docker.com/linux/ubuntu bionic/stable amd64 Packages
 docker-ce | 5:20.10.3~3-0~ubuntu-bionic | https://download.docker.com/linux/ubuntu bionic/stable amd64 Packages
 docker-ce | 5:20.10.2~3-0~ubuntu-bionic | https://download.docker.com/linux/ubuntu bionic/stable amd64 Packages
 docker-ce | 5:20.10.1~3-0~ubuntu-bionic | https://download.docker.com/linux/ubuntu bionic/stable amd64 Packages
 docker-ce | 5:20.10.0~3-0~ubuntu-bionic | https://download.docker.com/linux/ubuntu bionic/stable amd64 Packages
 docker-ce | 5:19.03.15~3-0~ubuntu-bionic | https://download.docker.com/linux/ubuntu bionic/stable amd64 Packages
 docker-ce | 5:19.03.14~3-0~ubuntu-bionic | https://download.docker.com/linux/ubuntu bionic/stable amd64 Packages
 docker-ce | 5:19.03.13~3-0~ubuntu-bionic | https://download.docker.com/linux/ubuntu bionic/stable amd64 Packages
 docker-ce | 5:19.03.12~3-0~ubuntu-bionic | https://download.docker.com/linux/ubuntu bionic/stable amd64 Packages
 docker-ce | 5:19.03.11~3-0~ubuntu-bionic | https://download.docker.com/linux/ubuntu bionic/stable amd64 Packages
 docker-ce | 5:19.03.10~3-0~ubuntu-bionic | https://download.docker.com/linux/ubuntu bionic/stable amd64 Packages
 docker-ce | 5:19.03.9~3-0~ubuntu-bionic | https://download.docker.com/linux/ubuntu bionic/stable amd64 Packages
 docker-ce | 5:19.03.8~3-0~ubuntu-bionic | https://download.docker.com/linux/ubuntu bionic/stable amd64 Packages
 docker-ce | 5:19.03.7~3-0~ubuntu-bionic | https://download.docker.com/linux/ubuntu bionic/stable amd64 Packages
 docker-ce | 5:19.03.6~3-0~ubuntu-bionic | https://download.docker.com/linux/ubuntu bionic/stable amd64 Packages
 docker-ce | 5:19.03.5~3-0~ubuntu-bionic | https://download.docker.com/linux/ubuntu bionic/stable amd64 Packages
 docker-ce | 5:19.03.4~3-0~ubuntu-bionic | https://download.docker.com/linux/ubuntu bionic/stable amd64 Packages
 docker-ce | 5:19.03.3~3-0~ubuntu-bionic | https://download.docker.com/linux/ubuntu bionic/stable amd64 Packages
 docker-ce | 5:19.03.2~3-0~ubuntu-bionic | https://download.docker.com/linux/ubuntu bionic/stable amd64 Packages
 docker-ce | 5:19.03.1~3-0~ubuntu-bionic | https://download.docker.com/linux/ubuntu bionic/stable amd64 Packages
 docker-ce | 5:19.03.0~3-0~ubuntu-bionic | https://download.docker.com/linux/ubuntu bionic/stable amd64 Packages
 docker-ce | 5:18.09.9~3-0~ubuntu-bionic | https://download.docker.com/linux/ubuntu bionic/stable amd64 Packages
 docker-ce | 5:18.09.8~3-0~ubuntu-bionic | https://download.docker.com/linux/ubuntu bionic/stable amd64 Packages
 docker-ce | 5:18.09.7~3-0~ubuntu-bionic | https://download.docker.com/linux/ubuntu bionic/stable amd64 Packages
 docker-ce | 5:18.09.6~3-0~ubuntu-bionic | https://download.docker.com/linux/ubuntu bionic/stable amd64 Packages
 docker-ce | 5:18.09.5~3-0~ubuntu-bionic | https://download.docker.com/linux/ubuntu bionic/stable amd64 Packages
 docker-ce | 5:18.09.4~3-0~ubuntu-bionic | https://download.docker.com/linux/ubuntu bionic/stable amd64 Packages
 docker-ce | 5:18.09.3~3-0~ubuntu-bionic | https://download.docker.com/linux/ubuntu bionic/stable amd64 Packages
 docker-ce | 5:18.09.2~3-0~ubuntu-bionic | https://download.docker.com/linux/ubuntu bionic/stable amd64 Packages
 docker-ce | 5:18.09.1~3-0~ubuntu-bionic | https://download.docker.com/linux/ubuntu bionic/stable amd64 Packages
 docker-ce | 5:18.09.0~3-0~ubuntu-bionic | https://download.docker.com/linux/ubuntu bionic/stable amd64 Packages
 docker-ce | 18.06.3~ce~3-0~ubuntu | https://download.docker.com/linux/ubuntu bionic/stable amd64 Packages
 docker-ce | 18.06.2~ce~3-0~ubuntu | https://download.docker.com/linux/ubuntu bionic/stable amd64 Packages
 docker-ce | 18.06.1~ce~3-0~ubuntu | https://download.docker.com/linux/ubuntu bionic/stable amd64 Packages
 docker-ce | 18.06.0~ce~3-0~ubuntu | https://download.docker.com/linux/ubuntu bionic/stable amd64 Packages
 docker-ce | 18.03.1~ce~3-0~ubuntu | https://download.docker.com/linux/ubuntu bionic/stable amd64 Packages
```

b. Install a specific version using the version string from the second column, 
```
    $ sudo apt-get install docker-ce=<VERSION_STRING> docker-ce-cli=<VERSION_STRING> containerd.io
```

- for example, 5:20.10.5~3-0~ubuntu-bionic from the list above "i.e. the output of command apt-cache".
```
    $ sudo apt-get install docker-ce=5:20.10.5~3-0~ubuntu-bionic docker-ce-cli=5:20.10.5~3-0~ubuntu-bionic containerd.io
```

- Verify that Docker Engine is installed correctly by running the hello-world image.
- This command downloads a test image and runs it in a container. 
- When the container runs, it prints an informational message and exits.
```
    $ sudo docker run hello-world
```
in case of error 
```
Cannot connect to the Docker daemon at unix:/var/run/docker.sock. Is the docker daemon running?

```

solution :
```
    $ sudo service --status-all 
    $ sudo service docker start

```

- Docker Engine is installed and running. 
- The docker group is created but no users are added to it. 
- You need to use sudo to run Docker commands. 
- Continue to Linux postinstall to allow non-privileged users to run Docker commands and for other optional configuration steps.

UPGRADE DOCKER ENGINE
- To upgrade Docker Engine, first run sudo apt-get update, 
- then follow the installation instructions, 
- choosing the new version you want to install.


