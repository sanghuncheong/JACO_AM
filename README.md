# JACO_AM
This repository is Arm move node for JACO robot.

JACO_AM is a ROS-node that let you plan the JACO arm using MoveIT(https://moveit.ros.org/).

To use this node you need to install MoveIT.

### Callback functions for ROS-topics
    
    # Below functions plan arm trajectory using the message protocol.
    rospy.Subscriber('check_goal_pose_msg', arm_move_msg, AM.check_goal_pose_m)
    rospy.Subscriber('move_goal_pose_msg', arm_move_msg, AM.move_goal_pose_m)
    rospy.Subscriber('move_goal_joint_msg', sensor_msgs.msg.JointState, AM.move_goal_joint_m)
    rospy.Subscriber('move_cartesian_goal_msg', arm_move_srv, AM.move_cartesian_goal_m)
    rospy.Subscriber('init_joints_msg', String, AM.init_joints_m)

    # Below functions set the environment that robot is planning using the message protocol.
    rospy.Subscriber('add_box_msg', box_info_msg, AM.add_box_m)
    rospy.Subscriber('del_box_msg', box_info_msg, AM.remove_box_m)
    rospy.Subscriber('att_box_msg', attach_hand_box, AM.attach_box_m)
    rospy.Subscriber('det_box_msg', box_info_msg, AM.detach_box_m)
    rospy.Subscriber('remove_all_msg', String, AM.remove_all_obj_m)

 