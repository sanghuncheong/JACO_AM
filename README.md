# JACO_AM
This repository is Arm move node for JACO robot.

JACO_AM is a ROS-node that let you plan the JACO arm using MoveIT(https://moveit.ros.org/).

To use this node you need to install MoveIT.

    def feasible_check_goalPose_m(self, data):

        # move_group = self.move_group
        move_group = moveit_commander.MoveGroupCommander(data.arm_name[0])
        pose_goal = geometry_msgs.msg.Pose()

        pose_goal.position = data.position
        pose_goal.orientation = data.orientation
        # move_group.set_planner_id('SPARStwo')
        # move_group.set_planner_id('RRTstar')
        # move_group.set_planner_id('BiTRRT')

        move_group.set_num_planning_attempts(10000)
        move_group.set_planning_time(5)
        move_group.set_goal_position_tolerance(0.01)
        move_group.set_goal_orientation_tolerance(0.01)

        move_group.set_pose_target(pose_goal)
        plan = move_group.plan()
        # print plan
        print "plan.joint_trajectory.joint_names :", plan.joint_trajectory.joint_names

        feasibility_flag_pub = self.feasibility_flag
        feasible_flag_msg = String()
        if len(plan.joint_trajectory.joint_names) == 0:
            print "no plan found"
            feasible_flag_msg = '0'
            feasibility_flag_pub.publish(feasible_flag_msg)
        elif len(plan.joint_trajectory.joint_names) > 0:
            print "plan found"
            feasible_flag_msg = '1'
            feasibility_flag_pub.publish(feasible_flag_msg)
            time.sleep(3)
            traj_arm_pub = self.traj_arm_publisher
            traj_arm_pub.publish(plan)

        time.sleep(2)
        move_group.stop()
        move_group.clear_pose_targets()

        current_pose = self.move_group.get_current_pose().pose
        return all_close(pose_goal, current_pose, 0.01)

    def move_goalPose_m(self, data):

        move_group = moveit_commander.MoveGroupCommander(data.arm_name[0])
        # move_group = self.move_group
        pose_goal = geometry_msgs.msg.Pose()

        pose_goal.position = data.goal_position
        pose_goal.orientation = data.goal_orientation
        # move_group.set_planner_id('SPARStwo')
        # move_group.set_planner_id('RRTstar')
        # move_group.set_planner_id('BiTRRT')

        move_group.set_num_planning_attempts(10000)
        move_group.set_planning_time(5)
        move_group.set_goal_position_tolerance(0.01)
        move_group.set_goal_orientation_tolerance(0.01)

        move_group.set_pose_target(pose_goal)

        print "goal pose:", pose_goal

        plan = move_group.plan()
        move_group.execute(plan, wait=True)
        traj_arm_pub = self.traj_arm_publisher
        traj_arm_pub.publish(plan)

        move_group.clear_pose_targets()

        current_pose = self.move_group.get_current_pose().pose
        return all_close(pose_goal, current_pose, 0.01)

    def move_goalJoints_m(self, data):

        self.group_name = data.name[0]  # this is just for the initialization
        print self.group_name, "planning group!!!!!!!!!!1"
        move_group = moveit_commander.MoveGroupCommander(self.group_name)
        joint_goal = move_group.get_current_joint_values()

        joint_goal[0] = data.position[0]
        joint_goal[1] = data.position[1]
        joint_goal[2] = data.position[2]
        joint_goal[3] = data.position[3]
        joint_goal[4] = data.position[4]
        joint_goal[5] = data.position[5]
        # joint_goal[6] = data.position[6]

        move_group.go(joint_goal, wait=True)
        move_group.stop()

        current_joints = move_group.get_current_joint_values()
        return all_close(joint_goal, current_joints, 0.01)

    def add_box_m(self, data, timeout=4):

        print "Start 'add box_m'", data.object_name[0]
        box_name = data.object_name[0]
        box_pose = geometry_msgs.msg.PoseStamped()
        box_pose.header.frame_id = "j2n6s300_link_base"

        box_pose.pose.position = data.object_position
        box_pose.pose.orientation = data.object_orientation

        box_scale = (data.object_scale.x, data.object_scale.y, data.object_scale.z)

        self.scene.add_box(box_name, box_pose, box_scale)

        self.box_name = box_name
        self.object_list.append(box_name)

        return self.wait_for_state_update(box_is_known=True, timeout=timeout)

    def attach_box_m(self, data, timeout=4):

        robot = self.robot
        scene = self.scene
        eef_link = self.eef_link
        group_names = self.group_names

        grasping_group = data.hand_name[0]
        touch_links = robot.get_link_names(group=grasping_group)
        print "touch links list\n", touch_links
        scene.attach_box(eef_link, data.box_name[0], touch_links=touch_links)

        return self.wait_for_state_update(box_is_attached=True, box_is_known=False, timeout=timeout)

    def detach_box_m(self, data, timeout=4):

        scene = self.scene
        eef_link = self.eef_link
        scene.remove_attached_object(eef_link, name=data.box_name[0])

        return self.wait_for_state_update(box_is_known=True, box_is_attached=False, timeout=timeout)

    def remove_box_m(self, data, timeout=4):

        scene = moveit_commander.PlanningSceneInterface()
        self.scene = scene
        self.box_name = data.object_name[0]
        scene.remove_world_object(self.box_name)

        return self.wait_for_state_update(box_is_attached=False, box_is_known=False, timeout=timeout)

    def remove_all_obj_m(self, data):
        print "remove all objects_m if 1, data:", data, type(data)
        if data.data == '1':
            print "remove all start"
            for i in tutorial.object_list:
                scene = moveit_commander.PlanningSceneInterface()
                self.scene = scene
                self.box_name = i

                scene.remove_world_object(self.box_name)