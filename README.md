# CarND-Path-Planning
Behavior planning and trajectory generation.

## Project Description
The goal of this project is to design a path planner that is able to create smooth, safe paths for the car to follow along a 3 lane highway with traffic. A successful path planner will be able to keep inside its lane, avoid hitting other cars, and pass slower moving traffic all by using localization, sensor fusion, and map data.

## Project files
The project includes the following folder/files:
- [src](https://github.com/SergeiDm/CarND-Path-Planning/tree/master/src) - the folder with c++ files with Path planning.
- [CMakeLists.txt](https://github.com/SergeiDm/CarND-Path-Planning/blob/master/CMakeLists.txt) - the file for building program.
- [illustrations]() - the folder with pictures for README.md.

## Dependencies
All dependencies can be found [here](https://github.com/udacity/CarND-Path-Planning-Project).

For project compilation [Eigen library files](http://eigen.tuxfamily.org/index.php?title=Main_Page) and [Spline header file](http://kluge.in-chemnitz.de/opensource/spline/) must be put in 'src' folder.

OS Windows 10 users may use [Bash on Ubuntu on Windows](https://msdn.microsoft.com/en-us/commandline/wsl/about) for dependencies installation and building program.

## Compiling and running the project
The project can be compiled and run by using the following command:
1. Make a build directory: `mkdir build && cd build`
2. Compile: `cmake .. && make`
3. Run it: `./path_planning`

## Project result
Below is the result video of this project.

<a href="https://youtu.be/xGXFW1g9OQ0" target="_blank"><img src="http://img.youtube.com/vi/xGXFW1g9OQ0/0.jpg" 
alt="IMAGE ALT TEXT HERE" width="400" height="300" border="10" /></a>

## Project explanation
### The Model
