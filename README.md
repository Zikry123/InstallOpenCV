# InstallOpenCV
script to install opencv
#!/bin/bash
# Install Open CV

yes | sudo apt-get update
#gives a list of updates available for the pre-installed packages/libraries

yes | sudo apt-get upgrade
#upgrades the pre-installed packages/libraries

sudo apt-get install build-essential cmake pkg-config
#load various image file formats from disc

sudo add-apt-repository "deb http://security.ubuntu.com/ubuntu xenial-security main"

sudo apt update

sudo apt install libjasper1 libjasper-dev

sudo apt-get install libjpeg8-dev libtiff5-dev libpng-dev

sudo apt-get install libavcodec-dev libavformat-dev libswscale-dev libv4l-dev

sudo apt-get install libxvidcore-dev libx264-dev

sudo apt-get install libgtk-3-dev
#installs libraries that are used to optimize various functionalities in OpenCV

sudo apt-get install libatlas-base-dev gfortran

sudo apt-get install python
#installs python

sudo apt-get install python2.7-dev python3.6-dev
#installs Python development headers and libraries for Python 2.7 and Python 3.6

cd ~
#change the directory

wget -O opencv.zip https://github.com/Itseez/opencv/archive/3.4.0.zip
#download the latest version

unzip opencv.zip
#opening the repository

wget -O opencv_contrib.zip https://github.com/Itseez/opencv_contrib/archive/3.4.0.zip

unzip opencv_contrib.zip
#full installation of OpenCV 3 to have access to features like SUFT AND SURF

cd ~
#change directory

wget https://bootstrap.pypa.io/get-pip.py

sudo python get-pip.py
#installs a Python package manager

sudo pip install virtualenv virtualenvwrapper
#install virtualenvwrapper and virtualenv

sudo rm -rf ~/get-pip.py ~/.cache/pip

# virtualenv and virtualenvwrapper

export WORKON_HOME=$HOME/.virtualenvs
#setting an environment variable called WORKN_HOME

source /usr/local/bin/virtualenvwrapper.sh
#load any necessary configurations from virtualenvwrapper

echo -e "\n# virtualenv and virtualenvwrapper" >> ~/.bashrc

echo "export WORKON_HOME=$HOME/.virtualenvs" >> ~/.bashrc

echo "source /usr/local/bin/virtualenvwrapper.sh" >> ~/.bashrc

source ~/.bashrc

mkvirtualenv cv -p python3
#create a python virtual environment named CV (computer vision)

workon cv
#Goes to the cv virtual environment

pip install numpy
#install numpy

workon cv

cd ~/opencv-3.4.0/

mkdir build

cd build

cmake -D CMAKE_BUILD_TYPE=RELEASE \
-D CMAKE_INSTALL_PREFIX=/usr/local \
-D WITH_CUDA=ON \
-D ENABLE_FAST_MATH=1 \
-D CUDA_FAST_MATH=1 \
-D CUDA_TOOLKIT_ROOT_DIR=/usr/local/cuda-9.1 \
-D WITH_CUBLAS=1 \
-D INSTALL_PYTHON_EXAMPLES=ON \
-D OPENCV_EXTRA_MODULES_PATH=~/opencv_contrib-3.4.0/modules \
-D PYTHON_EXECUTABLE=~/.virtualenvs/cv/bin/python \
-D CUDA_NVCC_FLAGS=--expt-relaxed-constexpr \
-D BUILD_EXAMPLES=ON \
-D INSTALL_PYTHON_EXAMPLES=ON \
-D INSTALL_C_EXAMPLES=OFF ..

ver=$(cat /proc/cpuinfo | awk '/^processor/{print $3}' | tail -1)
#finds the number of threads

make -j$ver

make

sudo make install

sudo ldconfig

#ls -l /usr/local/lib/python3.5/site-packages/
#total 1972
#-rw-r--r-- 1 root staff 2016816 Sep 13 17:24 cv2.cpython-35m-x86_64-linux-gnu.so

cd /usr/local/lib/python3.6/site-packages/

sudo mv cv2.cpython-35m-x86_64-linux-gnu.so cv2.so

cd ~/.virtualenvs/cv/lib/python3.6/site-packages/

ln -s /usr/local/lib/python3.6/site-packages/cv2.so cv2.so

$ cd ~
$ workon cv
$ python
Python 3.6.2 (default, Jul  5 2016, 12:43:10) 
[GCC 5.4.0 20160609] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import cv2
>>> cv2.__version__
'3.1.0'
>>>




