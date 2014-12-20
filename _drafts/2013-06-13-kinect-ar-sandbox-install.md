#On your own
Install X11 for OSX
Install XCode
Enable XCode command line utilities
Install Homebrew for OSX

#In a terminal
brew install libjpeg libpng libtiff libusb

#If they don't already exist
mkdir ~/src
mkdir ~/bin

cd ~/src

# Install VRUI, following the README file instructions

git clone ...
cd Vrui

#edit Vrui/Makefile, change INSTALLDIR to the bin directory
INSTALLDIR := $(HOME)/bin/Vrui-3.1

make -j2 (since I have two processors)
make install

#Confirm installed properly by running sample app
~/bin/Vrui-3.1/bin/XBackground

# Install Kinect, following the README file instructions

cd ~/src
git clone ...
cd Kinect

#edit Kinect/makefile, change VRUI_MAKEDIR to point to our install of VRUI
VRUI_MAKEDIR := $(HOME)/bin/Vrui-3.1/share/make

make

#Install executable to VRUI bin directory
cd /Users/twelch/bin/Vrui-3.1/bin

./bin/KinectUtil list
Kinect 0: Kinect for Xbox 1414   , USB address 020:011, device serial number B00366711208046B

./bin/KinectUtil getCalib 0
Downloading factory calibration data for Kinect B00366711208046B...
Depth conversion formula: dist[mm] = 345489 / (1089.41 - depth)

Depth unprojection matrix:
      0.00173667  0.00000000  0.00000000 -0.55573332
      0.00000000  0.00173667  0.00000000 -0.41679999
      0.00000000  0.00000000  0.00000000 -1.00000000
      0.00000000  0.00000000 -0.00000289  0.00315323
Depth-to-color pixel shift formula: Shift = 11.4115 - 13243.8/dist[mm]
Or: Shift = -30.3492 + 0.0383333*depth
Calculating best-fit color projection matrix for depth value range 399 - 975...
Smallest eigenvalue of color system = 0.00800861
Color matrix approximation RMS = 0.0873961
Optimal homography from world space to color image space:
      0.00143403 -0.00000577  0.00005954 -0.02763096
     -0.00000527  0.00190757 -0.00000003 -0.00375672
      0.00000000  0.00000000  0.00102564  0.00000000
     -0.00000763 -0.00001234 -0.00000007  1.00000000
Writing full intrinsic camera parameters to /Users/twelch/bin/Vrui-3.1/etc/Kinect-2.8/IntrinsicParameters-B00366711208046B.dat

# Install SARndbox

cd ~/src
git clone ...

#edit makefile, change VRUI_MAKEDIR to point to our install of VRUI, and INSTALLDIR to make it install in our bin directory
VRUI_MAKEDIR := $(HOME)/bin/Vrui-3.1/share/make
INSTALLDIR := $(HOME)/bin/SARndbox

make
make install

SARndbox not displaying when your projector is plugged in?  You probably have [this problem](https://discussions.apple.com/message/23487884#24471966).  Fix it by doing the following:
System Preferences->Mission Control
Uncheck "Displays have different spaces"

Step 1 and 2 - do not have to do, factory calibration will suffice
Step 3 - mount the projector :)
Step 4 - https://www.youtube.com/watch?v=9Lt4J_BErs0
Step 5 - https://www.youtube.com/watch?v=RmE6tkXoSJw
Step 6 - mount kinectd above sandbox
Step 7 - https://www.youtube.com/watch?v=vXkA9gUoSAc


orig - (-0.0076185, 0.0271708, 0.999602), -98.0000
new - (-0.00413144, 0.199811, 0.979826), -938.377

new 1st option - select 6, then go back and do 2-5 so stays in synch with video
2 - store grid

z key - hold and drag to recenter.  then zoom in and out

---- LINUX

KINECT

make
make install
make installudevrule
restart the system to load new udev rules

~/bin/Vrui-3.1/bin/KinectUtil list

---SARndbox-1.5

#edit makefile, change VRUI_MAKEDIR to point to our install of VRUI
VRUI_MAKEDIR := $(HOME)/bin/Vrui-3.1/share/make
