
I just hit this after doing a fresh install of DOCKER from the main docs. The problem for me was that immediately after the install, the service is not running.

These commands will help you to make sure docker is up and running for your run command to find it:

$ sudo service --status-all 
$ sudo service docker start
$ sudo service docker start

https://phoenixnap.com/kb/docker-on-raspberry-pi

Step 1: Update and Upgrade
Start by updating and upgrading the system. This ensures you install the latest version of the software.
Open a terminal window and run the command:

```
    $ sudo apt-get update && sudo apt-get upgrade
```
Step 2: Download the Convenience Script and Install Docker on Raspberry Pi
Move on to downloading the installation script with:
```
    $ curl -fsSL https://get.docker.com -o get-docker.sh
```
Execute the script using the command:
```
    $ sudo apt-get update
    $ sudo sh get-docker.sh
```

Step 3: Add a Non-Root User to the Docker Group
- By default, only users who have administrative privileges (root users) can run containers. 
- If you are not logged in as the root, one option is to use the sudo prefix.
- However, you could also add your non-root user to the Docker group which will allow it to execute docker commands.

- The syntax for adding users to the Docker group is:
```
    $ sudo usermod -aG docker [user_name]
```
- To add the Pi user (the default user in Raspbian), use the command:
```
    $ sudo usermod -aG docker Pi
```

- There is no specific output if the process is successful. For the changes to take place, you need to log out and then back in.

Step 4: Check Docker Version and Info
- Check the version of Docker on your Raspberry Pi by typing:
```
    $ docker version
```
The output will display the Docker version along with some additional information.
For system-wide information (including the kernel version, number of containers and images, and more extended description) run:
```
    $ docker info
```
Step 5: Run Hello World Container
The best way to test whether Docker has been set up correctly is to run the Hello World container.
To do so, type in the following command:
```
docker run hello-world
```
The software will contact the Docker daemon, pull the “hello-world” image, and create a new container based on that image.
