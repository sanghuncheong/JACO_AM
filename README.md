# JACO_AM

JACO_AM is a ROS-node that let you plan the JACO arm using [MoveIT](https://moveit.ros.org/). 

## Installation

You need to [install MoveIT](https://moveit.ros.org/install/) before install this package.


## Description

You can communicate with JACO_AM through both [ROS msg](https://github.com/sanghuncheong/JACO_AM/blob/tutorial/msg/README.md) and [ROS srv](https://github.com/sanghuncheong/JACO_AM/blob/tutorial/srv/README.md).



## Callback functions for ROS-topics
    
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

## Usage

```python
import foobar

foobar.pluralize('word') # returns 'words'
foobar.pluralize('goose') # returns 'geese'
foobar.singularize('phenomena') # returns 'phenomenon'
```

## Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

Please make sure to update tests as appropriate.

## License
[MIT](https://choosealicense.com/licenses/mit/)
