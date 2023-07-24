# ROS1 Mac OSX Support 
Developing on Mac OSX with ROS locally built for the past 6+ years has been nice, especially with the support scripts from [ros-install-osx](https://github.com/mikepurvis/ros-install-osx). Unfortunately, recently several `brew` commands are either failing or no longer supported to a point where building ROS on a Mac is not only frustrating, but extremely time consuming. The purpose of this repository is to hold a working copy of the libraries that has successfully built ROS on my Mac OSX machine. It's not elegant at all, in fact, it's very "hacky" and might clobber some existing `brew` packages on your machine. Regardless, I'm putting this together for my future self and the greater ROS community. That being said, I make no guarantees as to whether it will work for you. Good luck!

Notable ROS features that have been tested to work for development,
- ROS1 Kinetic (core, messages, actionlib, services) 
- OpenCV (3.3.1)
- PCL (1.8.1)
- Rviz (1.12.13)
- Qt (5.11.1), OGRE (1.9.0) 

The following OSX versions have been tested,
- Mac OS: Catalina (10.15.7)
- Mac OS: Sierra (circa 2019) 

## Instructions
- Download the `.zip` files I've conveniently stored on [Google Drive](https://drive.google.com/drive/folders/128wczlwCJNakNOX8ZSfXDFwe7Zl9UEhI?usp=share_link), I would advise you do this either via an Ethernet connection (or somewhere with fast WiFi, since the `*.zip` files are about 3GB). 
- Extract them directly into the desired directories,
```
unzip usr-local-boost-1-67.zip -d /usr/local/
unzip ros1-kinetic-mac-osx-catalina.zip -d /opt/
```

## Setup your `~/.bashrc`
You'll need to setup your `~/.bashrc` accordingly if you'll like to build your workspace using `catkin`. Append the following into your `~/.bashrc`

```
export PYTHONPATH=/usr/local/lib/python2.7/site-packages/
export LD_LIBRARY_PATH=/opt/ros/kinetic/lib
export LIBGL_ALWAYS_SOFTWARE=1s

source /opt/ros/kinetic/setup.bash
```
After you've done this, `source ~/.bashrc` and navigate to your `catkin` workspace and build like you normally would in Ubuntu using `catkin_make`. Personally, I like to see the build time and build with `clang` and `ninja` as follows,
```
time catkin_make -DCMAKE_BUILD_TYPE=Release -DCMAKE_C_COMPILER=/usr/bin/clang -DCMAKE_CXX_COMPILER=/usr/bin/clang++ -j8 --use-ninja;
```

## Known Issues
### Boost Upgrade 
There seems to be a `boost` incompatibility with the existing version built in the `.zip` due to [boost 1.67](https://github.com/phusion/passenger/issues/2213). I was able to fix this locally via forcefully upgrading inside `brew` to `1.76`, although apparently, it reportedly works for `1.69`, but I have yet to test this.
```
brew install boost@1.76
brew link --overwrite boost@1.76
```

## TODO (Mac OSX build with ROS2)
I have yet to try this, however, I did come across a decent [blog](http://www.robotandchisel.com/2020/08/10/rviz2-on-mac/) with some instruction demonstrating that this is indeed possible. 
