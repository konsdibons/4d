# Welcome to 4d
<p align="center">
  <img src="./apps/4d/icons/IconAssets.iconset/icon_512.png" width="400">
</p>

## 4d is a program for the processing of 4D-STEM data.
This is a collaborative project between the labs of Carsten Sachse, ER-C Jülich, Knut Müller-Caspary, LMU Munich, and Henning Stahlberg, EPFL Lausanne. 4d has inherited code from the focus-em.org project.

## Installation
### Getting the source code
The source code for 4d is available at our GITHUB repository. Use this to dowwload the lastest version:
> git clone https://github.com/LBEM-CH/4d.git

### Installing Dependencies
The dependencies for 4d are open source and free. They can be installed using standard package managers on various platforms. We recommend the following package managers for following operations systems:
- MacOS: brew (https://brew.sh)
- Ubuntu: apt-get
- Fedora/CentOS/RedHat: yum

### cmake
As we use cmake as build system you should have installed it on your machine. We advise to install this and most of the other dependencies by means of your native package manager. On OSX, for example, you could use “brew install cmake”. Alternatively, you can get cmake under the following link: http://www.cmake.org.
NOTE: Qt versions >= 5.7 (see below) will require a CMake version >= 3.1.0.

### g++ (incl. bindings)
The GUI is written in c++ with c++11 standards and requires a corresponding compiler. Again on some RedHat-like Linux distributions you need to install some bindings. On Fedora, we rely on the gcc-c++ package.

<ins>For MacOS</ins>, one would probably need to install packages like gcc using homebrew or macports. This could be done with “brew install gcc ; brew link gcc”. If done so, the following should be added to path:
> /usr/local/bin:/opt/bin:/opt/local/bin:/usr/bin/:/usr/sbin

Make sure that the gcc/g++ from the clang is not used to build otherwise it will fail. 

On OSX, you might have to do 
> cd /opt/homebrew/bin ; \ln -s g++-14 g++ ; \ln -s gcc-14 gcc

### libfftw3
This program requires fftw version 3.0.0 or later. The package is called libfftw3-dev on Ubuntu, but on Fedora you have to install fftw-devel and fftw-libs. You can install this famous library via the package manager or directly from http://www.fftw.org. In such a case use the following commands to compile FFTW:

> ./configure --enable-shared --enable-threads;

> make;

> sudo make install;

### Qt5
Compilations of Qt5 is included in all the package managers we listed above. Qt5 can also be downloaded and installed from: http://www.qt.io/download-open-source/
You also need the “qtscript5-dev - Qt 5 script development files”, which are not installed by default with Qt5. Installing the qtscript5-dev is also needed.
On Linux, the command
> sudo apt-get install qtscript5-dev

solves that problem.
Make sure that after the installation you add Qt5 bin directory to the environment variable $PATH, and that:
> qmake -query

gives you correct path to installed Qt libraries.

NOTE: Building with Qt versions >= 5.7 will require a CMake version >= 3.1.0.

NOTE for Mac OSX Users: Qt Version 5.9.4 worked fine, while Qt Version 5.10.1 caused the error: “build/apps/src/data/moc_ParameterConfiguration.cpp:175:63: error: 'init_priority' attribute is not supported on this platform.”

### Compiling 4d
Once everything is set up, CMAKE will automatically find the required paths and compile. This all has been scripted and 4d can  be compiled by running the build_all script, which take between zero and two arguments. The list below shows you all the possibilities:

- without arguments (./build_all): 4d will be built in the build directory inside source code and installed into ~/4d.
- with one argument (./build_all <dir>): You can specify your install and build location by passing an absolute path to the build script.
- with two arguments (./build_all <build_dir> <install_dir>): The build script with two arguments performs an out-of-place installation of 4d. The first passed absolute path corresponds to the build directory while the second defines the install directory.

4d is compiled in two stages. First we check the presence of all required dependencies and in the second stage we compile the entire source tree.

Upon building, 4d creates a directory “build”, in which the configuration and built files are placed. If compilation fails due to missing or wrong dependencies, and you add those dependencies later, then don't forget to remove the “build” directory before trying agaom to “./build_all”. Otherwise, the old configuration files in the “build” directory will still be present and steer the compilation into the wrong direction.

## The following external software tools are essential
The softwares in this category are required for the correct operation of 4d.

### (t)CSH

CSH is a Unix shell and a scripting language widely used in the electron microscopy field for historical reasons. One would not be able to run anything from 4d without CSH. 4d requires its successor, TCSH, which is better and safer. In modern Linux distributions, csh is just a symbolic link to tcsh. Please make sure this is the case in your system. If not please install tcsh >6.0 and make sure that csh links to it.

### gawk

gawk is a more powerful version of the command-line utility awk. 
- Install gawk on OSX with "brew install gawk". 
- On Linux, try “sudo apt-get install gawk”.

### Python and PILLOW

Many utilities and specific-purpose tools used by 4d are written in the Python scripting language (version 2.7.x). We recommend using a scientific Python installation like Anaconda or Canopy. You can also use the EMAN2.2 Python environment based on Anaconda (see below).

You also need **pip** and the module **pil** (or pillow).

On OSX, try

> xcode-select --install

> brew install python2.7

> pip3 install pillow

or alternatively:
> pip install pillow

On Linux, try:
> apt-get install python2.7 (or yum install python2.7)

> apt-get install python3

> pip3 install pillow

> pip3 install matplotlib

and make sure in the Preferences panel of 4d, that 4d is using this python2.7 binary, which may reside in /usr/local/bin/python2.7

Or to install those in python2.7:

> /usr/bin/python -mpip install -U pillow

> /usr/bin/python -mpip install -U matplotlib

### NumExpr
For accelerating some heavy calculations in Python scripts, 4d uses the NumExpr evaluator. You can install numexpr in your Python environment with the following pip command:
> pip install numexpr

## The following external software tools are optional
The following softwares are helpful for specific tasks. You need to install them, if you want to make use of them in your scripts.

### Software for drift correction
Drift correction can be done using MotionCor2. In case you require to do the drift correction using one of these software, please install the required software using the links below:
> MotionCor2: http://msg.ucsf.edu/em/software/motioncor2.html

> MotionCor3: https://github.com/czimaginginstitute/MotionCor3

> Unblur: http://grigoriefflab.janelia.org/unblur

> Zorro: https://github.com/LBEM-CH/zorro

### CTF determination software
In all projects, CTF can be determined for each frame using CTFFIND4 or for the averaged frame using gCTF. These softwares need to be installed separately from the links below, if you wish to use them.
> CTFFIND4: http://grigoriefflab.janelia.org/ctffind4

> GCTF: http://www.mrc-lmb.cam.ac.uk/kzhang/Gctf

### EMAN2

EMAN2 is a great package with lots of tools available. EMAN2 is easy to install and is available for MacOS and Linux on their website: http://blake.bcm.edu/emanwiki/EMAN2

If you want to use the EMAN2 python (that is python 2.7), then you can link that python in the 4d Preferences dialogue, on MacOS for example as /Applications/EMAN2/bin/python2.7 (or, where-ever you installed EMAN2).

If you compile 4d, make sure that the build_all script does not accidentally use the EMAN2 version of qmake. You can test this by typing in a terminal **which qmake**, or **qmake --version**, to see, which qmake shows up first in your path. If the EMAN2 qmake is taken first, you might want to rename that to a different qmake name, such as “qmake-4.8.7”.

### IMOD
We use many command line utilities present in IMOD. It can be downloaded from the website: http://bio3d.colorado.edu/imod/


