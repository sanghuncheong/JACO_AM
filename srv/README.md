# SERVICE PART

You can use service type messages to communicate with JACO_AM node.
There are 6 basic services in this folder.
If you want other *requests* or *responses*,
you may combine these to make your own service.:satisfied: HAVE FUN!

## Services
1. arm_goalJoint_srv: 
2. arm_move_joint_goal_srv: 

## Components

### request
**arm_name**: the name of the move group that you want to find the trajectory.\
**goalPose**: goal pose (position and orientation) for the planning\
**planner_name**: the name of the [OMPL planner](https://moveit.ros.org/documentation/planners/) that you want to use.
**n_attempt**: \
**c_time**: \
**n_repeat**: \
**start_state**: 

### response
**w_flag**: a flag value for checking if the service responded completely.\(1: work done, 0: error)\
**feasibility**: a flag value for checking the feasibility.(1: feasible, 0: NO PATH)\
**r_trj**: list of trajectory which is planned to goalPose with move-group.\
