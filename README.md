# mvbluefox3

mvBlueFOX3 library                         {#mainpage}
============

## Description

This library provides quick access to all the basic functions of Matrix Vision 
BlueFOX USB 3.0 cameras. 

## Installation

* Add the labrobotica repository if it is not already added:

Run the commands on _add repository_ and _add key_ from [labrobotica_how_to installation](https://gitlab.iri.upc.edu/labrobotica/labrobotica_how_to/-/blob/master/README.md#installation)

* Install the package:

``` sudo apt update && sudo apt install iri-mvbluefox3-dev ```

## Important information

- Matrix Vision driver. Download and install SDK (version 2.26 tested):

    - wget http://static.matrix-vision.com/mvIMPACT_Acquire/2.26.0/mvGenTL_Acquire-x86_64_ABI2-2.26.0.tgz
    - wget http://static.matrix-vision.com/mvIMPACT_Acquire/2.26.0/install_mvGenTL_Acquire.sh
    - chmod +x install_mvGenTL_Acquire.sh
    - ./install_mvGenTL_Acquire.sh -u


## Disclaimer  

Copyright (C) 2016-2019 Institut de Robòtica i Informàtica Industrial, CSIC-UPC.
Mantainer IRI labrobotics (labrobotica@iri.upc.edu)

This package is distributed in the hope that it will be useful, but without any warranty. It is provided "as is" without warranty of any kind, either expressed or implied, including, but not limited to, the implied warranties of merchantability and fitness for a particular purpose. The entire risk as to the quality and performance of the program is with you. should the program prove defective, the GMR group does not assume the cost of any necessary servicing, repair  or correction.

In no event unless required by applicable law the author will be liable to you for damages, including any general, special, incidental or consequential damages arising out of the use or inability to use the program (including but not limited to loss of data or data being rendered inaccurate or losses sustained by you or third parties or a failure of the program to operate with any other programs), even if the author has been advised of the possibility of such damages.

You should have received a copy of the GNU Lesser General Public License
along with this program.  If not, see <http://www.gnu.org/licenses/>


## Troubleshooting

### Configuring USBFS 

By default, Linux limits image capture buffers (e.g. to 16MB). 
If you run wxPropView in a terminal and opening the camera it complains about USBFS memory buffer, apply the following steps to set the memory limit to 1000MB:

1.  Open the `/etc/default/grub` file in any text editor. Find and replace: 

    `GRUB_CMDLINE_LINUX_DEFAULT="quiet splash"`

    with this:

    `GRUB_CMDLINE_LINUX_DEFAULT="quiet splash usbcore.usbfs_memory_mb=1000"`

2.  Update grub with these settings:

    `sudo update-grub`

3.  Reboot and test a USB 3.0 camera.

If this method fails to set the memory limit, run the following command:

`sudo sh -c 'echo 1000 > /sys/module/usbcore/parameters/usbfs_memory_mb'`

To confirm that you have successfully updated the memory limit, 
run the following command:

`cat /sys/module/usbcore/parameters/usbfs_memory_mb`

### No images received using original Matrix Vision software (wxPropView)

The original manufacturer driver has compatibility problems with some graphic cards. If you run the Matrix Vision software to setup the camera and no camera is detected, you might want to test older driver versions. An example could be using this one:

- As first step, uninstall all driver versions using the Matrix Vision software. Then, run the following:
    - `cd ~/Downloads`
    - `wget http://static.matrix-vision.com/mvIMPACT_Acquire/2.17.0/mvGenTL_Acquire-x86_64_ABI2-2.17.0.tgz -O mvGenTL_Acquire-x86_64_ABI2-2.17.0.tgz`
    - `wget https://www.matrix-vision.com/USB3-vision-camera-mvbluefox3.html?file=tl_files/mv11/support/mvIMPACT_Acquire/01/install_mvGenTL_Acquire.sh -O install_mvGenTL_Acquire.sh`
    - `sudo chmod +x install_mvGenTL_Acquire.sh`
    - `./install_mvGenTL_Acquire.sh`

## For developers

<details><summary>click here</summary>
<p>

## Dependencies

his package requires of the following system libraries and packages

 * [cmake](https://www.cmake.org "CMake's Homepage"), a cross-platform build system.
 * [doxygen](http://www.doxygen.org "Doxygen's Homepage") and [graphviz](http://www.graphviz.org "Graphviz's Homepage") to generate the documentation.
 * stdc++.

Under linux all of these utilities are available in ready-to-use packages.

Under MacOS most of the packages are available via [fink](http://www.finkproject.org/ "Fink's Homepage")

## Compilation and installation from source

Clone this repository and create a build folder inside:

``` mkdir build ```

Inside the build folder execute the following commands:

``` cmake .. ```

The default build mode is DEBUG. That is, objects and executables include debug information.

The RELEASE build mode optimizes for speed. To build in this mode execute instead
``` cmake .. -DCMAKE_BUILD_TYPE=RELEASE ```

The release mode will be kept until next time cmake is executed.

``` make -j $(nproc)``` 

In case no errors are reported, the generated libraries (if any) will be located at the
_lib_ folder and the executables (if any) will be located at the _bin_ folder.

In order to be able to use the library, it it necessary to copy it into the system.
To do that, execute

``` make install ```

as root and the shared libraries will be copied to */usr/local/lib/iri/mvbluefox3* directory
and the header files will be copied to */usr/local/include/iri/mvbluefox3* dierctory.
At this point, the library may be used by any user.

To remove the library from the system, exceute

``` make uninstall ```

as root, and all the associated files will be removed from the system.

To generate the documentation execute the following command:

``` make doc ```

## How to use it

To use this library in an other library or application, in the CMakeLists.txt file, first it is necessary to locate if the library has been installed or not using the following command

``` FIND_PACKAGE(mvbluefox3) ```

In the case that the package is present, it is necessary to add the header files directory to the include directory path by using

``` INCLUDE_DIRECTORIES(${mvbluefox3_INCLUDE_DIRS}) ```

and it is also necessary to link with the desired libraries by using the following command

``` TARGET_LINK_LIBRARIES(<executable name> ${mvbluefox3_LIBRARIES}) ```

## Examples

- To run the manufacturer GUI, execute the following command in a terminal:
  - `wxPropView` 
- There is one example called _mvbluefox3_test_. Check the console output message because in case of not having OpenCV 3.0 installed, the images won't be displayed but a message about successfull acquisition will be shown: 
  - `bin/mvbluefox3_test`

</p>
</details>

## Support material and multimedia

Please, visit: [**asantamaria's web page**](http://www.angelsantamaria.eu)mvBlueFOX3 library                         {#mainpage}
============

## Description

This library provides quick access to all the basic functions of Matrix Vision 
BlueFOX USB 3.0 cameras. 

## Installation

* Add the labrobotica repository if it is not already added:

Run the commands on _add repository_ and _add key_ from [labrobotica_how_to installation](https://gitlab.iri.upc.edu/labrobotica/labrobotica_how_to/-/blob/master/README.md#installation)

* Install the package:

``` sudo apt update && sudo apt install iri-mvbluefox3-dev ```

## Important information

- Matrix Vision driver. Download and install SDK (version 2.26 tested):

    - wget http://static.matrix-vision.com/mvIMPACT_Acquire/2.26.0/mvGenTL_Acquire-x86_64_ABI2-2.26.0.tgz
    - wget http://static.matrix-vision.com/mvIMPACT_Acquire/2.26.0/install_mvGenTL_Acquire.sh
    - chmod +x install_mvGenTL_Acquire.sh
    - ./install_mvGenTL_Acquire.sh -u


## Disclaimer  

Copyright (C) 2016-2019 Institut de Robòtica i Informàtica Industrial, CSIC-UPC.
Mantainer IRI labrobotics (labrobotica@iri.upc.edu)

This package is distributed in the hope that it will be useful, but without any warranty. It is provided "as is" without warranty of any kind, either expressed or implied, including, but not limited to, the implied warranties of merchantability and fitness for a particular purpose. The entire risk as to the quality and performance of the program is with you. should the program prove defective, the GMR group does not assume the cost of any necessary servicing, repair  or correction.

In no event unless required by applicable law the author will be liable to you for damages, including any general, special, incidental or consequential damages arising out of the use or inability to use the program (including but not limited to loss of data or data being rendered inaccurate or losses sustained by you or third parties or a failure of the program to operate with any other programs), even if the author has been advised of the possibility of such damages.

You should have received a copy of the GNU Lesser General Public License
along with this program.  If not, see <http://www.gnu.org/licenses/>


## Troubleshooting

### Configuring USBFS 

By default, Linux limits image capture buffers (e.g. to 16MB). 
If you run wxPropView in a terminal and opening the camera it complains about USBFS memory buffer, apply the following steps to set the memory limit to 1000MB:

1.  Open the `/etc/default/grub` file in any text editor. Find and replace: 

    `GRUB_CMDLINE_LINUX_DEFAULT="quiet splash"`

    with this:

    `GRUB_CMDLINE_LINUX_DEFAULT="quiet splash usbcore.usbfs_memory_mb=1000"`

2.  Update grub with these settings:

    `sudo update-grub`

3.  Reboot and test a USB 3.0 camera.

If this method fails to set the memory limit, run the following command:

`sudo sh -c 'echo 1000 > /sys/module/usbcore/parameters/usbfs_memory_mb'`

To confirm that you have successfully updated the memory limit, 
run the following command:

`cat /sys/module/usbcore/parameters/usbfs_memory_mb`

### No images received using original Matrix Vision software (wxPropView)

The original manufacturer driver has compatibility problems with some graphic cards. If you run the Matrix Vision software to setup the camera and no camera is detected, you might want to test older driver versions. An example could be using this one:

- As first step, uninstall all driver versions using the Matrix Vision software. Then, run the following:
    - `cd ~/Downloads`
    - `wget http://static.matrix-vision.com/mvIMPACT_Acquire/2.17.0/mvGenTL_Acquire-x86_64_ABI2-2.17.0.tgz -O mvGenTL_Acquire-x86_64_ABI2-2.17.0.tgz`
    - `wget https://www.matrix-vision.com/USB3-vision-camera-mvbluefox3.html?file=tl_files/mv11/support/mvIMPACT_Acquire/01/install_mvGenTL_Acquire.sh -O install_mvGenTL_Acquire.sh`
    - `sudo chmod +x install_mvGenTL_Acquire.sh`
    - `./install_mvGenTL_Acquire.sh`

## For developers

<details><summary>click here</summary>
<p>

## Dependencies

his package requires of the following system libraries and packages

 * [cmake](https://www.cmake.org "CMake's Homepage"), a cross-platform build system.
 * [doxygen](http://www.doxygen.org "Doxygen's Homepage") and [graphviz](http://www.graphviz.org "Graphviz's Homepage") to generate the documentation.
 * stdc++.

Under linux all of these utilities are available in ready-to-use packages.

Under MacOS most of the packages are available via [fink](http://www.finkproject.org/ "Fink's Homepage")

## Compilation and installation from source

Clone this repository and create a build folder inside:

``` mkdir build ```

Inside the build folder execute the following commands:

``` cmake .. ```

The default build mode is DEBUG. That is, objects and executables include debug information.

The RELEASE build mode optimizes for speed. To build in this mode execute instead
``` cmake .. -DCMAKE_BUILD_TYPE=RELEASE ```

The release mode will be kept until next time cmake is executed.

``` make -j $(nproc)``` 

In case no errors are reported, the generated libraries (if any) will be located at the
_lib_ folder and the executables (if any) will be located at the _bin_ folder.

In order to be able to use the library, it it necessary to copy it into the system.
To do that, execute

``` make install ```

as root and the shared libraries will be copied to */usr/local/lib/iri/mvbluefox3* directory
and the header files will be copied to */usr/local/include/iri/mvbluefox3* dierctory.
At this point, the library may be used by any user.

To remove the library from the system, exceute

``` make uninstall ```

as root, and all the associated files will be removed from the system.

To generate the documentation execute the following command:

``` make doc ```

## How to use it

To use this library in an other library or application, in the CMakeLists.txt file, first it is necessary to locate if the library has been installed or not using the following command

``` FIND_PACKAGE(mvbluefox3) ```

In the case that the package is present, it is necessary to add the header files directory to the include directory path by using

``` INCLUDE_DIRECTORIES(${mvbluefox3_INCLUDE_DIRS}) ```

and it is also necessary to link with the desired libraries by using the following command

``` TARGET_LINK_LIBRARIES(<executable name> ${mvbluefox3_LIBRARIES}) ```

## Examples

- To run the manufacturer GUI, execute the following command in a terminal:
  - `wxPropView` 
- There is one example called _mvbluefox3_test_. Check the console output message because in case of not having OpenCV 3.0 installed, the images won't be displayed but a message about successfull acquisition will be shown: 
  - `bin/mvbluefox3_test`

</p>
</details>

## Support material and multimedia

Please, visit: [**asantamaria's web page**](http://www.angelsantamaria.eu)
