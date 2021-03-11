Check your Linux distribution is using WSLv2: Open a Windows PowerShell and run:
```
    C:\WINDOWS\system32> wsl -l -v
    NAME      STATE           VERSION
    *Ubuntu    Running         2
 ```                   
Find the location of your VHDX file: First you need to find the distro app package directory, to achieve this open a Windows Powershell as Administrator and run:
```
    C:\WINDOWS\system32> Get-AppxPackage -Name "*Ubuntu*" | Select PackageFamilyName
    PackageFamilyName
    -----------------
    CanonicalGroupLimited.UbuntuonWindows_79abcdefgh
```
Your VHDX file path is: C:\Users\myuser\AppData\Local\Packages\CanonicalGroupLimited.UbuntuonWindows_79abcdefgh\LocalState\ext4.vhdx

Optimize your VHDX file: Open a Windows Powershell as Administrator to optimize your VHDX file, shutting down WSL first:
```
    C:\WINDOWS\system32> wsl --shutdown
    C:\WINDOWS\system32> optimize-vhd -Path C:\Users\myuser\AppData\Local\Packages\CanonicalGroupLimited.UbuntuonWindows_79abcdefgh\LocalState\ext4.vhdx -Mode full
```                            
A progress bar should be shown while optimizing the VHDX file, and storage should now be reflected correctly on the Windows Explorer.
You should now replace the PackageFamilyName and your user on the following path to find your VHDX file: C:\Users\user\AppData\Local\Packages\PackageFamilyName\LocalState\ For example:

    ls C:\Users\myuser\AppData\Local\Packages\CanonicalGroupLimited.UbuntuonWindows_79abcdefgh\LocalState\
    Mode                 LastWriteTime         Length Name
    -a----         3/14/2020   9:52 PM    57418973184 ext4.vhdx    
    
Note
The current implementation of WSLv2 does not have out-of-the-box access to external devices such as those connected through a USB port, but it automatically mounts your C: drive on /mnt/c/ (and others), which you can use to share deploy artifacts to be later flashed on hardware through Windows, but your build directory should not reside inside this mountpoint.
Once you have WSLv2 set up, everything is in place to develop just as if you were running on a native Linux machine. If you are going to use the Extensible SDK container, see the "Using the Extensible SDK" Chapter in the Yocto Project Application Development and the Extensible Software Development Kit (eSDK) manual. If you are going to use the Toaster container, see the "Setting Up and Using Toaster" section in the Toaster User Manual.
