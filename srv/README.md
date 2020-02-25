# SERVICE PART

You can use service type messages to communicate with JACO_AM node.
There are 6 basic services in this folder.
If you want other *requests* or *responses*,
you may combine these to make your own service.:satisfied: HAVE FUN!

## Services 함수 이름들 수정 필요합니다!
+ arm_goalJoint_srv: move_joints_s, 
+ arm_move_joint_goal_srv: 
+ arm_move_srv: goalPose_feasibility_check_s
+ att_hand_box_srv: att_box_s
+ box_info_srv: add_box_s, del_box_s, add_marker_box_s, del_marker_box_s, det_box_s
+ work_start_srv: jaco_init_joints_s, remove_all_s

## Components

### request
+ **work_start**: \
+ **arm_name**: the name of the move group that you want to find the trajectory.\
+ **hand_name**: \
+ **goalPose**: goal pose (position and orientation) for the planning\
+ **planner_name**: the name of the [OMPL planner](https://moveit.ros.org/documentation/planners/) that you want to use.
+ **n_attempt**: \
+ **c_time**: \
+ **n_repeat**: \
+ **start_state**: \ 
+ **object_name**: 그림이 필요할 수도 있겠다...\
+ **object_color**: \
+ **object_position**: \
+ **object_orientation**: \
+ **object_scale**: \

### response
+ **w_flag**: a flag value for checking if the service responded completely.\(1: work done, 0: error)\
+ **feasibility**: a flag value for checking the feasibility.(1: feasible, 0: NO PATH)\
+ **r_trj**: list of trajectory which is planned to goalPose with move-group.\
