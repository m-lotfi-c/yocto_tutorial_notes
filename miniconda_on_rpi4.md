refer to: https://stackoverflow.com/questions/39371772/how-to-install-anaconda-on-raspberry-pi-3-model-b

{USER}: pi

Install Miniconda 3:

wget http://repo.continuum.io/miniconda/Miniconda3-latest-Linux-armv7l.sh
sudo md5sum Miniconda3-latest-Linux-armv7l.sh # (optional) check md5
sudo /bin/bash Miniconda3-latest-Linux-armv7l.sh # -> change default directory to /home/pi/miniconda3
sudo nano /home/pi/.bashrc # -> add: export PATH="/home/pi/miniconda3/bin:$PATH"
sudo reboot -h now
Test:

conda
python --version
If Conda update miss permission of the directory:

sudo chown -R pi miniconda3
