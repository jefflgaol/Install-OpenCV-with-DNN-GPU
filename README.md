# Install-OpenCV-with-DNN-GPU
This guide will help you to build OpenCV (3.4.11) with DNN.
## Step 1: Remove previous existing OpenCV
```
$ sudo pip3 uninstall opencv-python
$ sudo pip uninstall opencv-python
```
And try to manually delete all OpenCV related files.
## Step 2: Install CUDA 10.0 and cuDNN
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
$ wget -O opencv.zip https://github.com/opencv/opencv/archive/3.4.11.zip
$ wget -O opencv_contrib.zip https://github.com/opencv/opencv_contrib/archive/3.4.11.zip
$ unzip opencv.zip
$ unzip opencv_contrib.zip
```
## Step 5: Build OpenCV source code
Remember to change CUDA_ARCH_BIN according your GPU computing capability (check: https://developer.nvidia.com/cuda-gpus). The minimum GPU computing capability is 5.3.
```
$ cd ~/opencv-3.4.11
$ mkdir build
$ cd build
$ cmake -D CMAKE_BUILD_TYPE=RELEASE \
	-D CUDA_NVCC_FLAGS=--expt-relaxed-constexpr \
	-D CMAKE_INSTALL_PREFIX=/usr/local \
	-D INSTALL_PYTHON_EXAMPLES=ON \
	-D INSTALL_C_EXAMPLES=OFF \
	-D OPENCV_ENABLE_NONFREE=ON \
	-D WITH_CUDA=ON \
	-D WITH_CUDNN=ON \
	-D OPENCV_DNN_CUDA=ON \
	-D ENABLE_FAST_MATH=ON \
	-D CUDA_FAST_MATH=ON \
	-D CUDA_ARCH_BIN=6.1 \
	-D WITH_CUBLAS=ON \
	-D OPENCV_EXTRA_MODULES_PATH=~/opencv_contrib-3.4.11/modules \
	-D HAVE_opencv_python3=ON \
	-D OPENCV_GENERATE_PKGCONFIG=ON \
	-D BUILD_EXAMPLES=ON \
	-D WITH_GSTREAMER=ON \
	-D WITH_GSTREAMER_0_10=OFF ..
$  make -j $(($(nproc) + 1))
```
## Step 6: Install OpenCV
```
$ sudo make install
$ sudo ldconfig
```
