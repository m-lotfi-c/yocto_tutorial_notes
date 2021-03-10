## How do I resolve unmet dependencies after adding a PPA?
```
reference & credit goto :
    https://askubuntu.com/questions/140246/how-do-i-resolve-unmet-dependencies-after-adding-a-ppa
```
Some packages could not be installed. This may mean that you have
requested an impossible situation or if you are using the unstable
distribution that some required packages have not yet been created
or been moved out of Incoming.
The following information may help to resolve the situation:

The following packages have unmet dependencies:
```
 package1 : Depends: package2 (>= 1.8) but 1.7.5-1ubuntu1 is to be installed
E: Unable to correct problems, you have held broken packages.
```
Here are some of its features:

search packages in all Launchpad PPAs
list and download packages in a PPA
add / remove / purge a PPA
backup and restore PPA sources
remove duplicate PPA sources
To install Y PPA Manager, open terminal by hitting Alt+Ctrl+T and run following commands:
````
sudo add-apt-repository ppa:webupd8team/y-ppa-manager
sudo apt-get update
sudo apt-get install y-ppa-manager
```
How can I resolve this?
--------------------------------------------------------------------------------------------------------------------------------------
## Answer:
--------------------------------------------------------------------------------------------------------------------------------------
- is a package management system for Debian and other Linux distributions based on it, such as Ubuntu. 
- For the most part, APT is easy to use for installing, removing, and updating packages. 
- In rare instances, often when you are mixing in third-party dependencies, 
- there is a chance that apt-get may end up giving you an error telling you that a package installation could not be completed.

This will show your sources.list:
```
cat /etc/apt/sources.list
```
This will show the list of PPAs (If any):
```
cat /etc/apt/sources.list.d/*
```
--------------------------------------------------------------------------------------------------------------------------------------
# Solutions:
--------------------------------------------------------------------------------------------------------------------------------------
- It is always a good idea to back up configuration files like /etc/apt/sources.list, so you can revert the changes if needed.
- If the error shows something like this:
```
  <some-package>: Depends: <other-package> (= version) but this-version is to be installed
```
- Then make sure that the restricted and universe repositories are enabled. 
- Hit Alt+F2, type software-properties-gtk and hit Enter.
- Under Ubuntu Software tab, enable all the repositories.
- One possible cause of unmet dependencies could be corrupted package database, and/or some packages weren’t installed properly. \

- To fix this problem, hit Alt+Ctrl+T to open terminal and try to run one of the following commands:
```
# 1 - try this
$ sudo apt-get clean
```
- apt-get clean clears out the local repository of retrieved package files (the .deb files).
- It removes everything but the lock file from /var/cache/apt/archives/ and /var/cache/apt/archives/partial/. 

or,

```
# 2 - try this
$ sudo apt-get autoclean
```
- apt-get autoclean clears out the local repository of retrieved package files, but unlike apt-get clean, 
- it only removes package files that can no longer be downloaded, and are largely useless.

One of the most basic fixes to resolve dependencies problems is to run:
```
# 3 - try this
sudo apt-get -f install
```
- The -f here stands for “fix broken”. 
- Apt will attempt to correct broken dependencies. 
- If you manually installed a package that had unmet dependencies, apt-get will install those dependencies, 
- if possible, otherwise it may simply remove the package that you installed in order to resolve the problem.
- Then run:
```
# 4 - try this
sudo dpkg --configure -a
```
- Then run this again:
```
# 5 - this should be okey
sudo apt-get -f install
```
- If the output is:
```
0 upgraded, 0 newly installed, 0 to remove and 1 not upgraded.
```
- That means it failed.

# Next solution is to run:
```
sudo apt-get -u dist-upgrade
```
- If it shows any held packages, it is best to eliminate them. 
- Packages are held because of dependency conflicts that apt cannot resolve. 
- Try this command to find and repair the conflicts:
```
sudo apt-get -o Debug::pkgProblemResolver=yes dist-upgrade
```
- If it cannot fix the conflicts, it will exit with:
```
0 upgraded, 0 newly installed, 0 to remove and 6 not upgraded.
```
- Delete the held packages one by one, running dist-upgrade each time, until there are no more held packages. 
- Then reinstall any needed packages. Be sure to use the --dry-run option, so that you are fully informed of consequences:
```
sudo apt-get remove --dry-run package-name
```

# Preventive Measures:

- So how can we avoid this from happening in the first place?
- Keep Ubuntu Up to date. 
- Ubuntu automatically notifies when updates are available, you can also check for available updates by clicking on Session Indicator in Unity panel:
- Or, Hit Alt+Ctrl+T to open terminal and run following commands:
```
sudo apt-get update
sudo apt-get upgrade
```
- Update: Synchronizes your list of available packages with the servers in source repositories. 
- Upgrade: Downloads & installs any newer versions of your installed packages.

- If you decide to add other repositories to sources.list, 
- make sure that the repository is meant to work (and known to work) with Ubuntu. 
- Repositories that are not designed to work with your version of Ubuntu can introduce inconsistencies in your system and might force you to re-install. 
- Also, make sure that you really need to add external repositories as the software package(s) 
