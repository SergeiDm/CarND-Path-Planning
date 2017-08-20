# CarND-Path-Planning
Behavior planning and trajectory generation.

## Project Description
The goal of this project is to design a path planner that is able to create smooth, safe paths for the car to follow along a 3 lane highway with traffic. A successful path planner will be able to keep inside its lane, avoid hitting other cars, and pass slower moving traffic all by using localization, sensor fusion, and map data.

## Project files
The project includes the following folder/files:
- [src](https://github.com/SergeiDm/CarND-Path-Planning/tree/master/src) - C++ files with Path planning implementation.
- [data](https://github.com/SergeiDm/CarND-Path-Planning/blob/master/data/highway_map.csv) - list of waypoints [x,y,s,dx,dy]:
  - x, y - the waypoint's map coordinate position,
  - s - distance along the road to get to that waypoint in meters,
  - dx, dy - the unit normal vector pointing outward of the highway loop.
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

The simulator which contains the Path Planning Project is [here](https://github.com/udacity/self-driving-car-sim/releases).

## Project result
Below is the result video of this project.

<a href="https://youtu.be/xGXFW1g9OQ0" target="_blank"><img src="http://img.youtube.com/vi/xGXFW1g9OQ0/0.jpg" 
alt="IMAGE ALT TEXT HERE" width="400" height="300" border="10" /></a>

## Project explanation
The project should generate a trajectory which satisfies the following criteria:
1. The car is able to drive at least 4.32 miles without incident.
2. The car doesn't drive faster than the speed limit (50 mph). Also the car isn't driving much slower than speed limit unless obstructed by traffic.
3. The car does not exceed a total acceleration of 10 m/s^2 and a jerk of 10 m/s^3.
4. The car must not come into contact with any of the other cars on the road.
5. The car doesn't spend more than a 3 second length out side the lane lanes during changing lanes, and every other time the car stays inside one of the 3 lanes on the right hand side of the road.
6. The car is able to smoothly change lanes when it makes sense to do so, such as when behind a slower moving car and an adjacent lane is clear of other traffic.

### Speed limit and acceleration
The initial car velocity is 0 mph. Whe incrementally increase velocity (lines 371-379 of 'main.cpp') if the current value is under 49.5 mph and there is no a slow moving car ahead. It allows us to meet criterion about acceleration.

In case of a slower moving car, we decrease the speed (lines 372-375).

Lines 268-293 calculate if there is a car in front of us on the same lane and the distance is less than 30 m. For defining this, the sensor data are used:
- ID - car's unique ID,
- x, y - car's x and y positions in map coordinates,
- vx, vy - car's x and y velocities in m/s,
- s - car's s position in frenet coordinates,
- d - car's d position in frenet coordinates.
Knowing our current lane, lane width (4 m.) and d values from sensor data, we can check if a car is in the same lane (line 276).

### Lane changing - making decision
In case of a slower moving car (lines 268-289), we should check possible lane changing. 

Lines 297-306 define successor states from initial state of our car. For example, if the current state is middle lane, so the next states may be middle or left or right lanes. To calculate next state/ lane, we use cost function (line 311) which is inversely proportional to:
- distance between our car and detected one,
- detected car's speed.

We loop over all possible successor states (lines 313-349) and calculate the same cost function (line 338-345), but if the distance (in term of s frenet coordinate) between our car and a car in next lane less than 5 m. we add a big number to the cost function (line 341), because collision is possible.

After comparing all cost functions (lines 351-356), we define the lane with the smallest cost function. Maybe it occurs that the current lane is the best now.

### Trajectory generation
Trajectory shoud be smooth

In this project for trajectory generation, the following approach was used:
1. Generate 3 points 













