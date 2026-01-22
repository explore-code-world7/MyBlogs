# wsl2
* window1
```bash
roscore
```
* window2
```bash
rviz
```

<img width="1400" height="1333" alt="image" src="https://github.com/user-attachments/assets/bedb433c-41c0-4350-b46a-6e467a77a380" />


# docker启用GUI支持
方案三：为 Docker 容器启用 GUI 支持（需要额外配置）
对于 Windows Docker Desktop：

需要安装 X11 服务器并配置 Docker 容器：

    安装 X11 服务器（如 VcXsrv）：

        下载地址：https://sourceforge.net/projects/vcxsrv/

        安装后启动 XLaunch，选择 "Disable access control"

    重新运行容器时添加显示参数：
    powershell

    # 停止并删除当前容器
    docker stop fd05d0c2a87a
    docker rm fd05d0c2a87a

    # 重新运行容器，添加显示参数
    docker run -it `
      --env="DISPLAY=host.docker.internal:0.0" `
      --env="QT_X11_NO_MITSHM=1" `
      -v /tmp/.X11-unix:/tmp/.X11-unix `
      -v C:\Users\firefox\catkin_ws:/home/catkin_ws `
      ros:melodic `
      /bin/bash

    在容器内安装必要的 GUI 依赖：
    bash

    apt-get update
    apt-get install -y x11-apps mesa-utils
    # 测试显示
    xeyes  # 应该能看到眼睛图案

对于 Linux 主机：
bash

docker run -it \
  --env="DISPLAY" \
  --env="QT_X11_NO_MITSHM=1" \
  --volume="/tmp/.X11-unix:/tmp/.X11-unix:rw" \
  -v /path/to/workspace:/home/catkin_ws \
  ros:melodic
