# ROS1 Mac OSX Support 
Developing on Mac OSX with ROS locally built for the past 6+ years has been nice, especially with the support scripts from [ros-install-osx](https://github.com/mikepurvis/ros-install-osx). However, recently, `brew` has been failing more and more commands to a point where building ROS on a Mac is not only frustrating but extremely time consuming. The purpose of this repository is to hold a working copy of the libraries that has successfully built ROS on my Mac OSX machine. It's not elegant at all, in fact, it's very "hacky". But I'm putting this together but for myself and the community, however, I make no guarantees as to whether it will work for you. 

Notable ROS components that have been tested to work for development,
- ROS1 Kinetic 
- OpenCV 3.3.1
- PCL
- Rviz
- Rqt

The following machnes have been tested,
- Mac OS: Catalina (10.15.7)
- Mac OS: Sierra (circa 2019) 

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
