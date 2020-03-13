# How-To-Install-OpenCV-with-DNN-GPU
This guide will help you to build OpenCV (4.2.0) with DNN.

## Step 1: Remove previous existing OpenCV
```
$ sudo pip3 uninstall opencv-python
$ sudo pip uninstall opencv-python
$ sudo apt-get purge *opencv*
$ sudo apt list --installed | grep opencv
```
## Step 2: Install CUDA and cuDNN
## Step 3: Install dependencies
```
$ sudo apt-get update
$ sudo apt-get upgrade
$ sudo apt-get install build-essential cmake unzip pkg-config
$ sudo apt-get install libjpeg-dev libpng-dev libtiff-dev
$ sudo apt-get install libavcodec-dev libavformat-dev libswscale-dev
$ sudo apt-get install libv4l-dev libxvidcore-dev libx264-dev
$ sudo apt-get install libgtk-3-dev
$ sudo apt-get install libatlas-base-dev gfortran
$ sudo apt-get install python3-dev
```
## Step 4: Download OpenCV source code
```
$ cd ~
$ wget -O opencv.zip https://github.com/opencv/opencv/archive/4.2.0.zip
$ wget -O opencv_contrib.zip https://github.com/opencv/opencv_contrib/archive/4.2.0.zip
$ unzip opencv.zip
$ unzip opencv_contrib.zip
```
## Step 5: Build OpenCV source code
Remember to change CUDA_ARCH_BIN according your GPU computing capability (check: https://developer.nvidia.com/cuda-gpus)
```
$ cd ~/opencv-4.2.0
$ mkdir build
$ cd build
$ cmake -D CMAKE_BUILD_TYPE=RELEASE \
	-D CMAKE_INSTALL_PREFIX=/usr/local \
	-D INSTALL_PYTHON_EXAMPLES=ON \
	-D INSTALL_C_EXAMPLES=OFF \
	-D OPENCV_ENABLE_NONFREE=ON \
	-D WITH_CUDA=ON \
	-D WITH_CUDNN=ON \
	-D OPENCV_DNN_CUDA=ON \
	-D ENABLE_FAST_MATH=1 \
	-D CUDA_FAST_MATH=1 \
	-D CUDA_ARCH_BIN=5.0 \
	-D WITH_CUBLAS=1 \
	-D OPENCV_EXTRA_MODULES_PATH=~/opencv_contrib/modules \
	-D HAVE_opencv_python3=ON \
	-D PYTHON_EXECUTABLE=~/.virtualenvs/opencv_cuda/bin/python \
	-D BUILD_EXAMPLES=ON \
	-D WITH_GSTREAMER=ON \
	-D WITH_GSTREAMER_0_10=OFF \
	-D WITH_QT=ON \
	-D WITH_OPENGL=ON ..
$ make -j16
```
## Step 6: Install OpenCV
```
$ sudo make install
$ sudo ldconfig
```
## Rebuild
```
$ cd ~/opencv-4.2.0
$ rm -rf build
$ mkdir build
$ cd build
```
and rebuild.
