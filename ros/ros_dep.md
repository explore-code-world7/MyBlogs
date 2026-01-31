
```bash
sudo apt install python-pip
sudo pip install rosdep
sudo rosdep init
sudo rosdep update
```

# ros安装第三方依赖
```bash
rosdep install -y   --from-paths ./3rdparty   --ignore-src
```
* 解析声明：rosdep 会扫描 ./3rdparty 目录下每个 ROS 包的 package.xml 文件，找到 <depend>, <exec_depend>, <build_depend> 等标签中列出的包名（例如 python3-numpy, libopencv-dev, boost）。
* 规则映射：rosdep 根据一个庞大的规则数据库（通常位于 /etc/ros/rosdep/ 或在线），将这些通用的 ROS 包名映射到当前操作系统（如 Ubuntu 22.04）上具体的软件包名（例如 ros-humble-navigation2 映射为一系列 apt 包）。
* 调用安装：最后，rosdep 调用系统包管理器（如 apt）执行安装命令。
