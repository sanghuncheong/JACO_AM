ROS messages used in JACO_AM node
=================================
1. arm_move_msg.msg
```markdown
- arm_name : The move group in the MoveIT that you are going to plan. 
- goal_position : The position of the goal pose (x, y, z).
- goal_orientation : The orientation of the goal pose in quaternion (x, y, z, w).
```
2. arm_move_obj_msg.msg
```markdown
- objects_name : 
- object_position
- object_orientation
- object_scale
- arm_name
- goal_position
- goal_orientation
```       
3. attach_hand_box.msg
4. box_info_msg.msg
