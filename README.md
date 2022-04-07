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
$ sudo pip3 install -U --no-deps numpy==1.19.4 future==0.18.2 mock==3.0.5 keras_processing==1.1.2 keras_applications==1.0.8 gast==0.4.0 protobuf pybind11 cython pkgconfig
```
**Step 4:** Install TensorFlow 2.7.0
```
$ sudo pip3 install --pre --extra-index-url https://developer.download.nvidia.com/compute/redist/jp/v461
```
## 3. Re-install corresponding OpenCV and fix bugs

## 4. Enable and demo Visionworks samples
