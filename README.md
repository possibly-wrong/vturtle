VPython-based robot simulator and turtle graphics engine
========================================================

Following are related blog posts:

* 2024-08-07: [Robot Simulator Updated to VPython 7.6.5](https://possiblywrong.wordpress.com/2024/08/07/robot-simulator-updated-to-vpython-7-6-5/)
* 2010-12-04: [Robot Simulator and Turtle Graphics, Revisited](https://possiblywrong.wordpress.com/2010/12/04/robot-simulator-and-turtle-graphics/)
* 2010-11-27: [A Robot Simulator Using VPython](https://possiblywrong.wordpress.com/2010/11/27/a-robot-simulator-using-vpython/)
* 2010-10-12: [Visual Python](https://possiblywrong.wordpress.com/2010/10/12/visual-python/)

This Python module simulates a three-wheeled robot that can execute Logo-like
motion commands. The robot is modeled after the
[Scribbler](https://en.wikipedia.org/wiki/Scribbler_(robot)), with a
cylindrical chassis with a hole in its center for inserting a colored marker,
which leaves a trail as the robot moves.

![Robot simulator example drawing a Koch snowflake](https://i.imgur.com/UKQAhWK.png)

With just this functionality, the module may be used as a turtle graphics
engine. The speed of animation of the robot's motion is configurable, from
"realistic" to "instantaneous." And thanks to [VPython](https://vpython.org/),
users can execute commands a line at a time from the interpreter prompt, and
rotate and zoom the 3D view of the robot, even while it is moving.

In addition, the robot has a stall sensor and configurable proximity sensors
for detecting and navigating around obstacles, such as walls or other robots.
There are convenience functions, `table()` for creating a simple table top
with four walled edges, and `maze()` for creating a simply connected maze.

![Robot simulator example in a maze](https://i.imgur.com/O0jY0AU.png)

Requirements
------------

Install [VPython](https://vpython.org/) e.g. with `pip install vpython`. This
code has been tested with VPython version 7.6.5 and Python versions 3.11 and
3.12.

Example code
------------

```
from vturtle import *
robot = Robot(obstacles=maze())
robot.forward(200) # run into wall
stalled = robot.stalled()
```

Robot commands
--------------

| Command          | Description                            | Example                                         |
|------------------|----------------------------------------|-------------------------------------------------|
| **forward**      | Move forward (cm)                      | `robot.forward(30)`                             |
| **backward**     | Move backward (cm)                     | `robot.backward(30)`                            |
| **left**         | Turn left (deg)                        | `robot.left(90)`                                |
| **right**        | Turn right (deg)                       | `robot.right(90)`                               |
| **pen_up**       | Pick up drawing pen                    | `robot.pen_up()`                                |
| **pen_down**     | Put down drawing pen                   | `robot.pen_down()`                              |
| **color**        | Get drawing pen color (r, g, b)        | `c = robot.color()`                             |
|                  | Set drawing pen color                  | `robot.color(color.red)`                        |
| **clear**        | Clear all drawing trails               | `robot.clear()`                                 |
| **show**         | Show robot                             | `robot.show()`                                  |
| **hide**         | Hide robot                             | `robot.hide()`                                  |
| **position**     | Get current (x,y) position (cm)        | `x, y = robot.position()`                       |
|                  | Move to (x,y) position (cm)            | `robot.position(60, 60)`                        |
| **heading**      | Get current heading (deg)              | `h = robot.heading()`                           |
|                  | Turn to heading (deg)                  | `robot.heading(270)`                            |
| **distance**     | Get distance to (x,y) position (cm)    | `d = robot.distance(-30, -30)`                  |
| **towards**      | Get heading to (x,y) position (deg)    | `h = robot.towards(-30, -30)`                   |
| **speed**        | Get robot speed (cm/s)                 | `s = robot.speed()`                             |
|                  | Set robot speed (cm/s)                 | `robot.speed(30)`                               |
|                  | Set robot speed to "instantaneous"     | `robot.speed(inf)`                              |
| **fast_forward** | Get animation speedup                  | `ff = robot.fast_forward()`                     |
|                  | Set animation speedup                  | `robot.fast_forward(2)`                         |
|                  | Set animation to "fastest possible"    | `robot.fast_forward(inf)`                       |
| **stalled**      | Get state of stall sensor (True/False) | `s = robot.stalled()`                           |
| **sensor**       | Get state of proximity sensor *id*     | `s = robot.sensor(id)`                          |
|                  | Get state of *left* proximity sensor   | `s = robot.sensor(0)`                           |
|                  | Get state of *front* proximity sensor  | `s = robot.sensor(1)`                           |
|                  | Get state of *right* proximity sensor  | `s = robot.sensor(2)`                           |
| **add_sensor**   | Add proximity sensor at bearing (deg)  | `id = robot.add_sensor(180)`                    |
| **sensor_range** | Get proximity sensor range (cm)        | `r = robot.sensor_range()`                      |
|                  | Set proximity sensor range (cm)        | `robot.sensor_range(5)`                         |
| **add_obstacle** | Register obstacle                      | `robot.add_obstacle(Wall((75, -75), (75, 75)))` |
