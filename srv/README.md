# SERVICE PART

You can use service type messages to communicate with JACO_AM node.
There are 6 basic services in this folder.
If you want other *requests* or *responses*,
you may combine these to make your own service.:satisfied: HAVE FUN!

## Description


### services
1. arm_goalJoint_srv: 
2. alwekmf

## components

### request
**arm_name**: the name of the move group that you want to find the trajectory.\
**goalPose**: goal pose (position and orientation) for the planning\

### response
**w_flag**: a flag value for checking if the service responded completely.
