# ROS msg used in JACO_AM node

You can use ROS msg to communicate with JACO_AM node.
There are 3 basic msgs in this folder.
If you want other msg,
you may combine these to make your own msg. :robot: HAVE FUN!

## msg 어떤 함수에서 쓰는지를 밝히는게 좋을지, 어떤 토픽에서 이용하는걸 밝히는게 좋을지 생각해보기
+ arm_move_msg: check_goal_pose_m, move_goal_pose_m, move_cartesian_goal_m,
+ att_hand_msg: att_box_m
+ box_info_msg: add_box_m, del_box_m, det_box_s

## Components

+ **arm_name** : The move group in the MoveIT that you are going to plan. 
+ **goal_position** : The position of the goal pose (x, y, z).
+ **goal_orientation** : The orientation of the goal pose in quaternion (x, y, z, w).
+ **planner_name** : \
+ **n_attempt** : \
+ **c_time** : \
+ **n_repeat** : \
+ **start_state** : \

### request 이 부분은 srv부분인데 참고할 사항들은 참고할것! 수정 필요
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
