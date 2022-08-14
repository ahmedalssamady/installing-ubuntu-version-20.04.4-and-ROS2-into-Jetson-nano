# installing-ubuntu-version-20.04.4-and-ROS2-into-Jetson-nano
installing-ubuntu-version-20.04.4-and-ROS2-into-Jetson-nano
# installing-ubuntu-version-20.04.4-and-ROS2-into-Jetson-nano

First I downloaded The virtual boxes version 6.1  , then created a new file named " ros_os1".
Downloaded the ubuntu version  20.04.4 and followed the instruction.
Opened the terminator and past the steps in this link to install ROS into the ubuntu 
http://wiki.ros.org/noetic/Installation/Ubuntu


1. Setup Ubuntu repositories
sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
2. Setup the keys
If you haven't already installed curl

sudo apt install curl
curl -s https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | sudo apt-key add -
3. Installation
Make sure the package is up to date

sudo apt update
Then pick which ROS you would like to install

Desktop-Full Install: (Recommended) : Everything in Desktop plus 2D/3D simulators and 2D/3D perception packages
sudo apt install ros-noetic-desktop-full
Desktop Install: Everything in ROS-Base plus tools like rqt and rviz
sudo apt install ros-noetic-desktop
ROS-Base: (Bare Bones) ROS packaging, build, and communication libraries. No GUI tools.
sudo apt install ros-noetic-ros-base
If we want to install a specific package we can use this command:

sudo apt install ros-noetic-PACKAGE NAME
Also, to find the other available packages, use:

apt search ros-noetic
4. Setup the enviroment
we should source this scipt in every bash terminal we use ROS in. but in my opinion, practically it's not convenient.

source /opt/ros/noetic/setup.bash
It will be more convenient to automatically source this script every time er launched a new shell. There are couple of commands that will do that for us.

Bash
echo "source /opt/ros/noetic/setup.bash" >> ~/.bashrc
source ~/.bashrc
Zsh
echo "source /opt/ros/noetic/setup.zsh" >> ~/.zshrc
source ~/.zshrc
5. Dependencies for building packages
To install the tool and other dependencies for building ROS packages, run:

sudo apt install python3-rosdep python3-rosinstall python3-rosinstall-generator python3-wstool build-essential
5.1. Initialize rosdep
If you have not yet installed rosdep, use:

sudo apt install python3-rosdep
Initialize rosdep and update it

sudo rosdep init
rosdep update


Taks 2

installing ROS2 into Jetson nano 

Installation steps
1. Set locale
Make sure that we have locale supports UTF-8

locale  
sudo apt update && sudo apt install locales 
sudo locale-gen en_US en_US.UTF-8  
sudo update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8  
export LANG=en_US.UTF-8  
2. Setup the sources
apt-cache policy | grep universe
3. Enable the Universe repository with the instructions.
sudo apt install software-properties-common
sudo add-apt-repository universe
4. Add ROS2 repository to the system
sudo apt update && sudo apt install curl gnupg2 lsb-release
sudo curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.key  -o /usr/share/keyrings/ros-archive-keyring.gpg
5. Add the repository to the sources list
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] http://packages.ros.org/ros2/ubuntu $(source /etc/os-release && echo $UBUNTU_CODENAME) main" | sudo tee /etc/apt/sources.list.d/ros2.list > /dev/null
6. Install ROS 2 packages
update the apt repository

sudo apt update
upgrade

sudo apt upgrade
Desktop Install: ROS, RViz, demos, tutorials.
sudo apt install ros-foxy-desktop
ROS-Base Install (Bare Bones): Communication libraries, message packages, command line tools. No GUI tools.
sudo apt install ros-foxy-ros-base
7. Setup the enviroment
Bash
echo "source /opt/ros/foxy/setup.bash" >> ~/.bashrc
source ~/.bashrc
Zsh
echo "source /opt/ros/foxy/setup.zsh" >> ~/.zshrc
source ~/.zshrc
