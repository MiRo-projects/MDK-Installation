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

## Specific setup instructions

Please see [the wiki](https://github.com/MiRo-projects/MDK-Installation/wiki) for more specific instructions on setting up your workstation to interact with MiRo. In particular, [this page](https://github.com/MiRo-projects/MDK-Installation/wiki/Running-code-on-MiRo-from-PyCharm) explains how to run code directly on a physical robot from your personal computer.

## Useful commands
The following commands all require a running `roscore` instance for use with a virtual MiRo.

**Launch the MiRo simulator:**
`~/mdk/sim/launch_sim.sh`

**Run the client GUI:**
`~/mdk/bin/shared/client_gui.py`

**Run the MiRo demo code:**
1. `cd ~/mdk/share/python/miro2/core`
2. `./client_demo.py - caml & client_demo.py - camr & client_demo.py`

## Troubleshooting
Running the client GUI (found at `~/mdk/bin/shared/client_gui.py`) is often a good first step to check if you are able to communicate properly with MiRo (either virtual or physical). You should be able to view camera images, see touch sensor activation, and send commands to the motor system, speakers, and lights.

If you can view ROS data but not send commands, this usually indicates that `ROS_IP` is not set correctly.