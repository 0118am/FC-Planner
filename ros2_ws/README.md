# ROS2 Workspace

This directory provides a partial ROS2 port of **FC-Planner**. Currently only the
`quadrotor_msgs` package has been translated to ROS2.

## Building

```bash
source /opt/ros/humble/setup.bash
colcon build --symlink-install
```

Additional packages need to be ported before the full system can run under ROS2.
