# JACO_AM
This repository is Arm move node for JACO robot.

JACO_AM is a ROS-node that let you plan the JACO arm using MoveIT(https://moveit.ros.org/).

To use this node you need to install MoveIT.

### List of ROS messages and services types
    
1. arm_move_msg.msg
```buildoutcfg
    string[] arm_name : The move group in the MoveIT that you are going to plan. 
    geometry_msgs/Point goal_position : The position of the goal pose (x, y, z).
    geometry_msgs/Quaternion goal_orientation : The orientation of the goal pose in quaternion (x, y, z, w).
```       
2. arm_move_obj_msg.msg
```buildoutcfg

```

### Callback functions for ROS-topics
    
    feasible_check_goalPose_m:
    
    move_goalPose_m:

    move_goalJoints_m:

    add_box_m:

    attach_box_m:

    detach_box_m:

    remove_box_m:

    remove_all_obj_m:
 