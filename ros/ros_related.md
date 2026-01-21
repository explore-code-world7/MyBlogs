# Ros-noetic

## install

1. replace source package
   https://robotics.stackexchange.com/questions/99013/ros-cannot-install-noetic-due-to-unmet-dependencies-20-04
2. install
   https://wiki.ros.org/noetic/Installation/Ubuntu

# ROS2

## install

* solution = https://docs.ros.org/en/rolling/Installation/Ubuntu-Install-Debs.html
* remember to sudo update&upgrade with recommended updates

# Start an ros env
## 1. activate ros command package 
```bash
source /opt/ros/melodic/setup.bash   # 18.04
source /opt/ros/noetic/setup.bash   # 20.04
source /opt/ros/humble/setup.bash   # 22
```

# 2. initialize catkin workspace env
```bash
# 进入你的工作空间根目录
cd ~/catkin_ws
# 编译
catkin_make
# 初始化工作空间环境（将覆盖系统环境中同名的包）
source devel/setup.bash
```
