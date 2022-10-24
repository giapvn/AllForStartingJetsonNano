# All For Starting Jetson Nano
Guide to install all critical components for beginning with Jetson Nano
## 1. How to flash Jetpack 4.6.1 and some tips
**Step 1:** Download "SD Card Image" at this link https://developer.nvidia.com/embedded/jetpack.</br>
**Step 2:** Prepare a SD card reader. Download Etcher tool to flash Jetpack to SD card at this link https://www.balena.io/etcher/.</br>
**Step 3:** Push SD card to Jetson Nano board and plug in power. And then do follow guideline as shown on the screen.</br>
In order to use Jetson Nano in the highest performance(10W) setup your module with this mode:</br>
`$ sudo nvpmode -m 0`</br>
In order to save more RAM, let instead of the current desktop by a light desktop such that:</br>
`$ sudo apt install lxde lxdm`</br>
And then restart your module and experience the new desktop.
If you cannot open terminal by using the keystroke of `Ctrl +  Alt + t`, you will configure this keystroke in the `lxde-rc.xml` file as follows:</br>
```
$ cd ~/.config/openbox
$ sudo gedit lxde-rc.xml
```
Insert the below lines to the file and then save it.</br>
```
<!-- Keybindings for running terminal -->
  <keybind key="C-A-t">
      <action name="Execute">
          <command>lxterminal</command>
      </action>
  </keybind>
```
Finally, run this conmand:</br>
`$ sudo openbox --reconfigure`</br>
Now, the OS was installed completely.
## 2. Install TensorFlow compatible with Jetpack version
At the present, Jetpack version 4.6.1 is compatible with version 2.7.0 of Tensorflow. Hereafter we start to install Tensorflow 2.7.0.</br>
**Step 1:** Install system packages required by Tensorflow:
```
$ sudo apt-get update
$ sudo apt-get install libhdf5-serial-dev hdf5-tools libhdf5-dev
$ sudo apt-get install zlib1g-dev zip libjpeg8-dev liblapack-dev libblas-dev gfortran
```
**Step 2:** Install and upgrade pip3:
```
$ sudo apt-get install python3-pip
$ sudo pip3 install -U pip testresources setuptools==49.6.0
```
**Step 3:** Install Python package dependencies
```
$ sudo pip3 install -U --no-deps numpy==1.19.4 future==0.18.2 mock==3.0.5 keras_processing==1.0.5 keras_applications==1.0.8 gast==0.4.0 protobuf pybind11 cython pkgconfig
```
**Step 4:** Install TensorFlow 2.7.0
```
$ sudo pip3 install --pre --extra-index-url https://developer.download.nvidia.com/compute/redist/jp/v461
```
## 3. Re-install corresponding OpenCV and fix bugs
Here, I will download source and install OpenCV in version 4.1.1. </br>
**Step 1:** Let's remove the other OpenCV:</br>
`$ sudo sudo apt-get purge *libopencv*`</br>
**Step 2:** Install dependencies:</br>
```
$ sudo apt-get update
$ sudo apt-get install -y build-essential cmake git libgtk2.0-dev pkg-config libavcodec-dev libavformat-dev libswscale-dev
$ sudo apt-get install -y libgstreamer1.0-dev libgstreamer-plugins-base1.0-dev
$ sudo apt-get install -y python2.7-dev python3.6-dev python-dev python-numpy python3-numpy
$ sudo apt-get install -y libtbb2 libtbb-dev libjpeg-dev libpng-dev libtiff-dev libdc1394-22-dev
$ sudo apt-get install -y libv4l-dev v4l-utils qv4l2 v4l2ucp
$ sudo apt-get install -y curl
```
**Step 3:** Download OpenCV (I will save them in a directory as called `/installer`):</br>
```
$ cd installer/
$ mkdir opencv
$ cd opencv/
$ curl -L https://github.com/opencv/opencv/archive/4.4.1.zip -o opencv-4.4.1.zip
$ curl -L https://github.com/opencv/opencv_contrib/archive/4.4.1.zip -o opencv_contrib-4.4.1.zip
```
**Step 4:** Build OpenCV:</br>
```
$ unzip opencv-4.1.1.zip
$ unzip opencv_contrib-4.4.1.zip
$ cd opencv-4.1.1/
$ mkdir build
$ cd build/
$ cmake -D WITH_CUDA=ON -D WITH_CUDNN=ON -D CUDA_ARCH_BIN="5.3,6.2,7.2" -D CUDA_ARCH_PTX="" -D OPENCV_GENERATE_PKGCONFIG=ON -D OPENCV_EXTRA_MODULES_PATH=../../opencv_contrib-4.1.1/modules -D WITH_GSTREAMER=ON -D WITH_LIBV4L=ON -D BUILD_opencv_python2=ON -D BUILD_opencv_python3=ON -D BUILD_TESTS=OFF -D BUILD_PERF_TESTS=OFF -D BUILD_EXAMPLES=OFF -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/usr/local ..
$ make -j4
$ sudo make install
$ sudo ldconfig
```
Now we have just installed completely OpenCV4 on Jetson Nano. However, you can reach some glitches while using it such as:</br>
### You cannot include eigen3 libs with same syntax as used in older versions</br>
How  to fix it?</br>
```
$ cd /usr/include
$ sudo ln -sf eigen3/Eigen Eigen
$ sudo ln -sf eigen3/unsupported unsupported
```
### You cannot include opencv4 libs with same syntax as used in older versions</br>
```
$ sudo cp -r /usr/local/include/opencv4/opencv2/ /usr/include/
```
## 4. Enable and demo Visionworks samples
