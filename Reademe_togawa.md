## Project: 3D Motion Planning
![Quad Image](./misc/enroute.png)

---

### Writeup / README

### Starter Code

`motion_planning.py` works almost same as `backyard_flyer_solution.py`

In `motion_planning.py` is added `PLANNING` state to calculate path before take off, `backyard_flyer_solution.py` create box shape flight path after take off.

In `plan_path` function,
 1. make grid representation of a 2D configuration space given obstacle data with target_altitude and safety_distance.
 2. Set start location as center of the map and goal location is 10m North and 10m East.
 3. Seach free space path with  A* algoritm
 4. Conveert path to waypoints to adding north and eat offset.
 5. end waypoints to simulator and takeoff.


![Top Down View](./misc/high_up.png)

#### 1. Set your global home position
Read `colliders.csv` first line and convert csv to lat and lon float number.

    float(home_pos_data[1].strip().split(" ")[1])

#### 2. Set your current local position
Global position is set in `[self._longitude, self._latitude, self._altitude]`
Use `global_to_local` fucntion to get local position.

#### 3. Set grid start position from local position
Get a grid and north and east offset for a particular altitude and safety margin around obstacles
Set start point from current location `int(local_pos[0]-north_offset), int(local_pos[1]- east_offset)`

#### 4. Set grid goal position from geodetic coords
Picked up [-122.400886, 37.795174] as goal location from the simulator.
Convert global latitude longitude location to location position with `global_to_local` function.


#### 5. Modify A* to include diagonal motion (or replace A* altogether)
Added diagonal motion to Action enum in `planning_utils.py` file.
define cost of diagonal motion to sqrt(2)

    NE = (-1, 1,np.sqrt(2))
    SE = ( 1, 1,np.sqrt(2))
    SW = ( 1,-1,np.sqrt(2))
    NW = (-1,-1,np.sqrt(2))

and `valid_actions`

    if x - 1 < 0 or y - 1 < 0 or grid[x-1,y-1] == 1:
        valid_actions.remove(Action.NW)
    if x - 1 < 0 or y + 1 > m or grid[x-1,y+1] == 1:
        valid_actions.remove(Action.NE)
    if x + 1 > n or y - 1 < 0 or grid[x+1,y-1] == 1:
        valid_actions.remove(Action.SW)
    if x + 1 > n or y + 1 > m or grid[x+1,y+1] == 1:
        valid_actions.remove(Action.SE)

#### 6. Cull waypoints
Prune path to minimize number of waypoints

Added `prune_path` function in `motion_planning.py` remove collinear series of points to make efficient waypoints.


### Execute the flight
#### 1. Does it work?
It works!
