Installing GCC on debain-based system
-The default Ubuntu repositories contain a meta-package named build-essential that contains the GCC compiler and 
- a lot of libraries and other utilities required for compiling software.

-Start by updating the packages list:
```
$ sudo apt update
```

-Install the build-essential package by typing:
```
$ sudo apt install build-essential
```
The command installs a bunch of new packages including gcc, g++ and make.

You may also want to install the manual pages about using GNU/Linux for development:

sudo apt-get install manpages-dev
To validate that the GCC compiler is successfully installed, use the gcc --version command which prints the GCC version:

gcc --version
The default version of GCC available in the Ubuntu 18.04 repositories is 7.4.0:

gcc (Ubuntu 7.4.0-1ubuntu1~18.04) 7.4.0
Copyright (C) 2017 Free Software Foundation, Inc.
This is free software; see the source for copying conditions.  There is NO
warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
That’s it. GCC is now installed on your system, and you can start using it.


Installing Multiple GCC Versions
This section provides instructions about how to install and use multiple versions of GCC on Ubuntu 18.04. The newer versions of the GCC compiler include support for new languages, better performance and extended features.

At the time of writing this article, the default Ubuntu repositories include several GCC versions, from 5.x.x to 8.x.x. The latest version of GCC, which is 9.1.0 is available from the Ubuntu Toolchain PPA.

In the following example, we will install the latest three versions of GCC and G++.

First, add the ubuntu-toolchain-r/test PPA to your system with:

sudo apt install software-properties-common
sudo add-apt-repository ppa:ubuntu-toolchain-r/test
Install the desired GCC and G++ versions by typing:

sudo apt install gcc-7 g++-7 gcc-8 g++-8 gcc-9 g++-9
The commands below will configure alternative for each version and associate a priority with it. The default version is the one with the highest priority, in our case that is gcc-9.

sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-9 90 --slave /usr/bin/g++ g++ /usr/bin/g++-9 --slave /usr/bin/gcov gcov /usr/bin/gcov-9
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-8 80 --slave /usr/bin/g++ g++ /usr/bin/g++-8 --slave /usr/bin/gcov gcov /usr/bin/gcov-8
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-7 70 --slave /usr/bin/g++ g++ /usr/bin/g++-7 --slave /usr/bin/gcov gcov /usr/bin/gcov-7
Later if you want to change the default version use the update-alternatives command:

sudo update-alternatives --config gcc
There are 3 choices for the alternative gcc (providing /usr/bin/gcc).

  Selection    Path            Priority   Status
------------------------------------------------------------
* 0            /usr/bin/gcc-9   90        auto mode
  1            /usr/bin/gcc-7   70        manual mode
  2            /usr/bin/gcc-8   80        manual mode
  3            /usr/bin/gcc-9   90        manual mode

Press <enter> to keep the current choice[*], or type selection number:
You will be presented with a list of all installed GCC versions on your Ubuntu system. Enter the number of the version you want to be used as a default and press Enter.

The command will create symbolic links to the specific versions of GCC and G++.
