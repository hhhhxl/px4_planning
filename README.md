# px4_planning

#### 介绍
基于PX4实现无人机的轨迹规划与轨迹跟踪控制

#### 软件架构
软件架构说明

#### 安装教程
安装nlopt优化库
```
sudo apt-get install ros-melodic-nlopt
```
protoc版本: 3.0.0

PX4-Autopilot版本:v1.11.1

下载编译
```
git clone https://gitee.com/MrZhaosx/px4_planning.git
cd px4_planning
catkin_make
```

#### 使用说明

```
#启动仿真环境
roslaunch gazebo_px4_simulation empty_px4vision.launch

#启动规划算法
roslaunch gazebo_px4_simulation kino_replan_gazebo.launch
roslaunch plan_manage rviz.launch

#启动控制算法（attitude_controller算法）
roslaunch gazebo_px4_simulation attitude_controller.launch
#仿真时 gazebo_simulation = true
#实际飞行时 gazebo_simulation = false

#在rviz上用(2D Nav Goal)触发 
注：轨迹的形状修改 px4_planning/src/trajectory_generator/waypoint_generator/src/sample_waypoints.h
```

----------------------------------- 以下用于调试控制器参数 ----------------------------------------
1. 调试attitude_controller参数
```
启动仿真环境
roslaunch gazebo_px4_simulation empty_px4vision.launch

#启动控制器
roslaunch gazebo_px4_simulation attitude_controller.launch

#启动轨迹生成算法
roslaunch gazebo_px4_simulation trajectory_generator.launch
roslaunch gazebo_px4_simulation trajectory_rviz.launch
在rviz上用(2D Nav Goal)触发(即，向/goal话题发布内容) 启动规划

启动调试小工具
rosrun attitude_controller err_show.py
```

2. 调试PID参数

```
启动仿真环境
roslaunch gazebo_px4_simulation empty_px4vision.launch


#启动控制器
roslaunch pid_controller controller.launch
##启动无人机
rostopic pub /uav/remote/cmd std_msgs/UInt8 "data: 1"
##降落无人机
rostopic pub /uav/remote/cmd std_msgs/UInt8 "data: 2"


#启动轨迹生成算法
roslaunch gazebo_px4_simulation trajectory_generator.launch
roslaunch gazebo_px4_simulation trajectory_rviz.launch
在rviz上用(2D Nav Goal)触发(即，向/goal话题发布内容) 启动规划


启动跟踪误差显示工具
rosrun attitude_controller err_show.py
启动动态调参工具
rosrun rqt_reconfigure rqt_reconfigure 
```
