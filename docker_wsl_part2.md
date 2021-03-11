- Verify that Docker Engine is installed correctly by running the hello-world image.
- This command downloads a test image and runs it in a container. 
- When the container runs, it prints an informational message and exits.
```
    $ sudo docker run hello-world
```
output:
```
Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/
```

# in case of error:
```
    docker: Cannot connect to the Docker daemon at unix:///var/run/docker.sock. Is the docker daemon running?.
    See 'docker run --help'.
```
solution :
```
    $ sudo service --status-all 
    $ sudo service docker start
    $ sudo docker run hello-world
```

UPGRADE DOCKER ENGINE
- To upgrade Docker Engine, download the newer package file and repeat the installation procedure, pointing to the new file.
- Install using the convenience script
- Docker provides convenience scripts at get.docker.com and test.docker.com for installing edge and testing versions of 
- Docker Engine - Community into development environments quickly and non-interactively. 
- The source code for the scripts is in the docker-install repository. 
- Using these scripts is not recommended for production environments, and 
- you should understand the potential risks before you use them:
  - The scripts require root or sudo privileges to run. 
  - Therefore, you should carefully examine and audit the scripts before running them.
  - The scripts attempt to detect your Linux distribution and version and configure your package management system for you. 
  - In addition, the scripts do not allow you to customize any installation parameters. This may lead to an unsupported configuration, 
  - either from Docker’s point of view or from your own organization’s guidelines and standards.
  - The scripts install all dependencies and recommendations of the package manager without asking for confirmation. 
  - This may install a large number of packages, depending on the current configuration of your host machine.
  - The script does not provide options to specify which version of Docker to install, and 
  - installs the latest version that is released in the “edge” channel.
  - Do not use the convenience script if Docker has already been installed on the host machine using another mechanism.
  - This example uses the script at get.docker.com to install the latest release of Docker Engine - Community on Linux. 
  - To install the latest testing version, use test.docker.com instead. 
  - In each of the commands below, replace each occurrence of get with test.

Warning:

    Always examine scripts downloaded from the internet before running them locally.

```
    $ curl -fsSL https://get.docker.com -o get-docker.sh
    $ sudo sh get-docker.sh
```

- If you would like to use Docker as a non-root user, you should now consider adding your user to the “docker” group with something like:
```
    $ sudo usermod -aG docker <your-user>
```
example :
```
    $ sudo usermod -aG docker $USER
```
- Remember to log out and back in for this to take effect!
