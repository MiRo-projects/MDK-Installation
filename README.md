# MDK installation
Start here: Setting up the MDK for MiRo project development

## Getting started
There’s just a couple of things to do before starting your project:
1. Request access to this group in the Slack and accept the invite
2. Create a repo for your project, and clone it to a sensible place in the MDK folder.
  * `~/mdk/share/python/miro2/<your-project>` is probably a good location
  * We suggest using GitHub to manage your project files because the lab machines in B.09 are not managed by the University; they’re not backed up, anybody can log in, and the data on them today is not guaranteed to be there tomorrow. A Git repo is an easy way to manage your data, track your changes and ensure your work is available anywhere, but if you prefer another method to secure and access your work then you may use that instead.

That's it! If you've not used Git before then there's a couple of guides linked below, or ask if you need any help.
* [Resources to learn Git](https://try.github.io)
* [Guides to various Git concepts](https://guides.github.com)
* [Git commands cheatsheet](https://github.github.com/training-kit/downloads/github-git-cheat-sheet/)

## Using the MDK
### In the lab
The computers in B.09 already have all the necessary software installed and configured so you can write and test code on either a physical or virtual MiRo robot. In either case, you will need to configure some environment variables to get everything working: 

| Variable          | Physical                   | Virtual                  |
| ----------------- | -------------------------- | ------------------------ |
| `ROS_IP`          | Your computer's local IP   | Your computer's local IP |
| `ROS_MASTER_URI`  | `http://<MiRo's IP>:11311` | `http://localhost:11311` |
| `MIRO_ROBOT_NAME` | The robot's ROS name       | `miro`                   |

You can view a physical robot's ROS name by using the [Android app](https://play.google.com/store/apps/details?id=com.consequentialrobotics.miroapp_2p0). The recommended way to set these variables is to edit `~/.miro2/config/user_setup.bash`; check that none of them have been overridden in `~/.bashrc`.

If you are using PyCharm, ensure that the system environment variables have been inherited by the IDE. If they have not, a list of all required variables you can copy and update as needed is below.

### On your personal computer
We use [ROS](https://www.ros.org) to interface with both physical and virtual MiRos and [Gazebo](http://gazebosim.org) as a simulation environment, so these are the two additional software packages you'll need to test your code on your personal machine. There are two ways to get going:

#### Native
A native install will allow the Gazebo simulator to run quicker and is likely to be simpler and have fewer issues overall, but because of the software dependencies it will require you to install [Ubuntu 16](http://releases.ubuntu.com/16.04/) or an Ubuntu 16 fork such as [Linux Mint 'Sylvia'](https://linuxmint.com/release.php?id=31) as your OS.

Once you've done that, it's recommended you follow the [official MiRo-E documentation](http://labs.consequentialrobotics.com/miro-e/docs/index.php?page=Developer_Profiles_Simulator) for installing ROS Kinetic and Gazebo 7.

#### Docker
If you don't want to install Ubuntu 16 on your machine, it should be possible to run a virtualised instance of the MiRo simulator through [Docker](https://www.docker.com) (as long as you're still running some Linux variant). [Install Docker CE](https://docs.docker.com/install/linux/docker-ce/ubuntu/) and then:
1. Run `docker pull tacd/miro_sim` to get the MiRo simulator Docker image
2. Run `docker run -it --net host -v $XAUTHORITY:/root/.Xauthority -v /tmp/.X11-unix:/tmp/.X11-unix tacd/miro_sim` to launch the Docker image

Alternatively, see the [macOS installation guide](https://github.com/MiRo-projects/MDK-Installation/blob/master/Installation/MDK%20installation%20on%20MAC%20OS.pdf) for installation on that platform.

### Useful commands
The following commands all require a running `roscore` instance for use with a virtual MiRo

**Launch the MiRo simulator:**
`~/mdk/sim/launch_sim.sh`

**Run the client GUI:**
`~/mdk/bin/shared/client_gui.py`

**Run the MiRo demo code:**
1. `cd ~/mdk/share/python/miro2/core`
2. `./client_demo.py - caml & client_demo.py - camr & client_demo.py`

### Environment variables
If PyCharm is not inheriting the system environment variables, it may be easier to copy and paste this list instead of trying to wrangle the PyCharm launcher into behaving. Note that the first five variables will need to be updated according to your desired configuration.
```
MIRO_STATIC_IP=127.0.0.1
MIRO_ROBOT_NAME=miro
ROS_IP=127.0.0.1
ROS_MASTER_IP=localhost
ROS_MASTER_URI=http://localhost:11311

MIRO_DIR_TRASH=/home/miro/.miro2/trash
MIRO_NETWORK_MODE=static
MIRO_DIR_PID=/tmp/miro2/pid
MIRO_DIR_STATE=/run/user/1001/miro2/state
MIRO_DIR_LOG=/tmp/miro2/log
MIRO_SPEAK_IP=1
MIRO_DYNAMIC_IP_MATCH=^[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}$
MIRO_DIR_DUMP=/tmp/miro2/dump
MIRO_DIR_SHARE=/home/miro/mdk/share
MIRO_MDK_RELEASE=R191016
MIRO_DIR_MDK=/home/miro/mdk
MIRO_EDITION=2
MIRO_TOKEN=miro2
MIRO_DIR_ONBOARD=/home/miro/mdk/bin/onboard
MIRO_MULTITOOL=/home/miro/mdk/bin/onboard/multitool.sh
MIRO_DIR_CONFIG=/home/miro/.miro2/config
MIRO_DIR_TMP=/tmp/miro2
MIRO_DYNAMIC_IP_WAIT=30
MIRO_DIR_BIN=/home/miro/mdk/bin/arm32
MIRO_ROS_RELEASE=kinetic
MIRO_DIR_USER=/home/miro/.miro2
MIRO_USER_SETUP=/home/miro/.miro2/config/user_setup.bash
MIRO_BRIDGE_FLAGS=l
MIRO_SYSTEM=arm32
ROS_ETC_DIR=/opt/ros/kinetic/etc/ros
ROS_ROOT=/opt/ros/kinetic/share/ros
ROS_VERSION=1
ROS_PACKAGE_PATH=/home/miro/mdk/catkin_ws/install/share:/opt/ros/kinetic/share
ROS_DISTRO=kinetic
PYTHONPATH=/home/miro/mdk/share/python:/home/miro/mdk/catkin_ws/install/lib/python2.7/dist-packages:/opt/ros/kinetic/lib/python2.7/dist-packages
LD_LIBRARY_PATH=/home/miro/mdk/catkin_ws/install/lib:/opt/ros/kinetic/lib
NODE_PATH=:/home/miro/.local/npm/lib/node_modules
PKG_CONFIG_PATH=/home/miro/mdk/catkin_ws/install/lib/pkgconfig:/opt/ros/kinetic/lib/pkgconfig
```

### Troubleshooting
If you can view ROS data but not send commands, this usually indicates that `ROS_IP` is not set correctly.
