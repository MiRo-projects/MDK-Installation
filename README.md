# MDK installation
Start here: Setting up the MDK for MiRo project development

## Getting started
There’s just a couple of things to do before starting your project:
1. Request access to this group in the Slack and accept the invite
2. Create a repo for your project, and clone it to a sensible place in the MDK folder. `~/mdk/share/python/miro2/your-project` is probably a good location
  * We suggest using GitHub to manage your project files because the lab machines in B.09 are not managed by the University; they’re not backed up, anybody can log in, and the data on them today is not guaranteed to be there tomorrow. A Git repo is an easy way to manage your data, track your changes and ensure your work is available anywhere, but if you have another preferred method to secure and access your work then you may use that instead.

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

### Troubleshooting
If you can view ROS data but not send commands, this usually indicates that `ROS_IP` is not set correctly.
