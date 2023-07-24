# ROS1 Mac OSX Support 
The purpose of this repository is to hold a working copy of the libraries that has successfully built ROS1 on my Mac OSX machine. I'm putting this together both for myself and the community as every time I attempt to rebuild from source via (https://github.com/mikepurvis/ros-install-osx)[ros-install-osx], some annoying `brew` issues always seems to occur. After getting frustrated for the N'th time, I figured just zipping up the entire set of `brew`'d items under `/usr/local/` is the quickest, dumbest, thing that seems to be fairly reliable. I have not yet tested any other OS versions, nor have I tested on any other machine, therefore, I make no guarantees as to whether it will work for you. However, I have performed this "hack" several times and have successfully ran ROS1 locally with OpenCV, PCL, Rviz, RQT all functional on my Mac. An older machine has built this successfully on Sierra as well. So good luck!

The following my current machine versions:
- Mac OS: Catalina (10.15.7)
- ROS1 Kinetic 

## Instructions
- Download the `.zip` files I've conveniently stored on (https://drive.google.com/drive/folders/128wczlwCJNakNOX8ZSfXDFwe7Zl9UEhI?usp=share_link)[Google Drive].
- Extract them directly into the desired directories,
```
unzip usr-local-boost-1-67.zip -d /usr/local/
unzip ros-kinetic-mac-osx-catalina.zip -d /opt/
```


## Setup your `~/.bashrc`
You'll need to setup your `~/.bashrc` accordingly if you'll like to build your workspace using `catkin`, therefore append the following into your `~/.bashrc`

```
export PYTHONPATH=/usr/local/lib/python2.7/site-packages/
export LD_LIBRARY_PATH=/opt/ros/kinetic/lib
export LIBGL_ALWAYS_SOFTWARE=1s

source /opt/ros/kinetic/setup.bash

```


## Known Issues
### Boost Upgrade 
There seems to be a `boost` incompatibility with the target `boost` built in the `.zip` due to (https://github.com/phusion/passenger/issues/2213)[boost1.67]. I was able to fix this locally via forcefully upgrading inside `brew` to `1.76`, however, it reportedly works for `1.69`

```
brew install boost@1.76
brew link --overwrite boost@1.76
```