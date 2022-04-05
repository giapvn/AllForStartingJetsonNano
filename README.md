# All For Starting Jetson Nano
Guide to install all critical components for beginning with Jetson Nano
## 1. How to flash Jetpack 4.6.1 and some tips
**Step 1:** Download "SD Card Image" at this link https://developer.nvidia.com/embedded/jetpack.</br>
**Step 2:** Prepare a SD card reader. Download Etcher tool to flash Jetpack to SD card at this link https://www.balena.io/etcher/.</br>
**Step 3:** Push SD card to Jetson Nano board and plug in power. And then do follow guideline as shown on the screen.</br>
In order to use Jetson Nano in the highest performance(10W) setup your module with this mode:</br>
`sudo nvpmode -m 0`</br>
In order to save more RAM, let instead of the current desktop by a light desktop such that:</br>
`sudo apt install lxde lxdm`</br>
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
Now, the OS was installed conpletely.
## 2. Install TensorFlow compatible with Jetpack version

## 3. Re-install corresponding OpenCV and fix bugs

## 4. Enable and demo Visionworks samples
