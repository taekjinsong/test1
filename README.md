# test1


ssh ghost@192.168.168.105

First, we activate the shell file for publishing detection and tracking modules.  
Please downloads the git files and builds the ros1 package (catkin build) for image topics.

```
git clone TrackingHuman_ver01.git

cd TrackingHuman_ver01/ros1_ws; ross; catkin b
```

The shell file 'tracking.sh' runs the detection and tracking using track_id_ros.cpp including yolo and bytetrack engine files.

```
./tracking.sh
```

We use ROS bridge for converting the detection information to control the robot using ROS2.
ROS bridge MUST require both ROS1 and ROS2 environments before compiling ROS bridge. 

```
cd ../..
source /home/ghost/.ros1rc
source /home/ghost/.ros2rc
```

Then, builds custom_bridge package using colcon build and executes the custom_bridge_node. 

```
cd TrackingHuman_ver01/ros2_ws
colcon build --packages-select custom_bridge
source install/setup.bash
ros2 run custom_bridge custom_bridge_node &> /home/ghost/custom_bridge.log &
```

Moves to the scripts folder of ros2_ws and runs the .py file using python3 command.

```
cd ../..
cd TrackingHuman_ver01/ros2_ws/scripts
ros2s; python3 control_human_tracking_ver2.py
```

open the new terminal and publishes ros2 topic to assign the specific id like belows. 

```
ros2s; ros2 topic pub -1 /activate_tracking std_msgs/msg/String "{data: '1'}"
```
