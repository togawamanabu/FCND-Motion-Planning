## Project: 3D Motion Planning
![Quad Image](./misc/enroute.png)

---

### Writeup / README

#### 1. Provide a Writeup / README that includes all the rubric points and how you addressed each one.  You can submit your writeup as markdown or pdf.  

You're reading it! Below I describe how I addressed each rubric point and where in my code each point is handled.

### Explain the Starter Code

#### 1. Explain the functionality of what's provided in `motion_planning.py` and `planning_utils.py`

Added `PLANNING` state in `motion_planning.py` to plan path after armed and before take off, in `backyard_flyer_solution.py` create box shape flight path after take off.

In `plan_path` function, 1. make grid representation of a 2D configuration space given obstacle data. this is create_grid function in `planning_utils.py`  2. create path with a star algorithm given grid,  heuristic, start and goal position.this is a_star function in `create_grid`.




![Top Down View](./misc/high_up.png)


#### 1. Set your global home position

#### 2. Set your current local position

#### 3. Set grid start position from local position

#### 4. Set grid goal position from geodetic coords

#### 5. Modify A* to include diagonal motion (or replace A* altogether)

#### 6. Cull waypoints

### Execute the flight
#### 1. Does it work?
It works!
