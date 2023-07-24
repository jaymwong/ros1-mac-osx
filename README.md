# ROS1 Mac OSX Support 
Developing on Mac OSX with ROS locally built for the past 6+ years has been nice, especially with the support scripts from [ros-install-osx](https://github.com/mikepurvis/ros-install-osx). However, recently, `brew` has been failing more and more commands to a point where building ROS on a Mac is not only frustrating but extremely time consuming. The purpose of this repository is to hold a working copy of the libraries that has successfully built ROS on my Mac OSX machine. It's not elegant at all, in fact, it's very "hacky" and might clobber some existing `brew` packages on your machine. Regardless, I'm putting this together for my future self and the greater ROS community. That being said, I make no guarantees as to whether it will work for you. Good luck!

Notable ROS components that have been tested to work for development,
- ROS1 Kinetic 
- OpenCV (3.3.1)
- PCL (1.8.1)
- Rviz (1.12.13)
- Qt (5.11.1), OGRE (1.9.0) 

The following OSX versions have been tested,
- Mac OS: Catalina (10.15.7)
- Mac OS: Sierra (circa 2019) 

## Instructions
- Download the `.zip` files I've conveniently stored on [Google Drive](https://drive.google.com/drive/folders/128wczlwCJNakNOX8ZSfXDFwe7Zl9UEhI?usp=share_link).
- Extract them directly into the desired directories,
```
unzip usr-local-boost-1-67.zip -d /usr/local/
unzip ros-kinetic-mac-osx-catalina.zip -d /opt/
```

## Setup your `~/.bashrc`
You'll need to setup your `~/.bashrc` accordingly if you'll like to build your workspace using `catkin`. Append the following into your `~/.bashrc`

```
export PYTHONPATH=/usr/local/lib/python2.7/site-packages/
export LD_LIBRARY_PATH=/opt/ros/kinetic/lib
export LIBGL_ALWAYS_SOFTWARE=1s

source /opt/ros/kinetic/setup.bash
```
After you've done this, `source ~/.bashrc` and navigate your `catkin` workspace and build like you normally would in Ubuntu using `catkin_make`. Personally, I like to see the build time and build with `clang` and `ninja` as follows,
```
time catkin_make -DCMAKE_BUILD_TYPE=Release -DCMAKE_C_COMPILER=/usr/bin/clang -DCMAKE_CXX_COMPILER=/usr/bin/clang++ -j8 --use-ninja;
```

## Known Issues
### Boost Upgrade 
There seems to be a `boost` incompatibility with the target `boost` built in the `.zip` due to [boost1.67](https://github.com/phusion/passenger/issues/2213). I was able to fix this locally via forcefully upgrading inside `brew` to `1.76`, apparently, it reportedly works for `1.69`, but I have yet to test this.
```
brew install boost@1.76
brew link --overwrite boost@1.76
```

## TODO (ROS2)
Yes, I know ROS1 Kinetic is EOL and no longer supported. Yes, I know Ubuntu 16.04 is EOL and no longer support. And by definition, any development we do on Mac OSX using Kinetic to deploy with Ubuntu 16.04 in production is, by nature not supported. Yet, we've deployed multiple robots in production at @SouthieAutonmy using this architecture with several workarounds to overcome the drawbacks for ROS1. Again, not elegant. However, this is definitely a form of tech debt I want you to know, if you are to proceed with this route. I've been meaning to eventually get around to a successful ROS2 build on my Mac, but again, this is technically unsupported as well and has been much more difficult to wrap my head around compared to ROS1 source build.  -- Jay M. Wong (2023)
