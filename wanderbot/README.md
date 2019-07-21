# wanderbot
## enviroment
Ubuntu 18.04 + ROS melodic and **set the enviroment variable**
```
export TURTLEBOT3_MODEL=burger
```
## simulation
Terminal 1:
```
roslaunch turtlebot3_gazebo turtlebot3_world.launch
```
Terminal 2:
```
rosrun wanderbot red_light_green_light.py 
```

