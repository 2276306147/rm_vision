# ***君瞄宝宝速成教程***

## 0 Introduction

### 0.0 rm_vision
此处缺图

### 0.1 Overview
- &emsp;rm_vision 项目旨在为 RoboMaster 队伍提供一个规范、易用、鲁棒、高性能的视觉框架方案，为 RM 开源生态的建设添砖加瓦
- &emsp;如果本开源项目对于贵战队的视觉技术发展起到了实质性的帮助作用，请在机器人上贴上以下标签以助力该项目的推广，十分感激！

### 0.2 唯一交流群

- QQ交流群 ：君已走
- 群里各种大佬，帅男靓女，先行跪谢

### 0.3 包含项目

- 装甲板自动瞄准算法模块 <https://github.com/chenjunnn/rm_auto_aim>
- MindVision 相机模块 <https://github.com/chenjunnn/ros2_mindvision_camera>
- HikVision 相机模块 <https://github.com/nolem-77/ros2_hik_camera>
- 机器人云台描述文件 <https://github.com/chenjunnn/rm_gimbal_description>
- 串口通讯模块 <https://github.com/chenjunnn/rm_serial_driver>
- 视觉算法仿真器 <https://github.com/chenjunnn/rm_vision_simulator>

## 1 Preparations

### 1.0 运行设备
- > NUC &emsp;可以很推荐
- > TX2 &emsp;有点可以有点推荐
- > Nano &emsp;新版有点可以有点推荐 | 旧版有点不可以有点点推荐
- > RaspberryPi &emsp;没有可以不推荐

### 1.1 部署条件

- > 网络很ok，建议开 *6G* 
- > 足够不傻，希望 *不出bug*

### 1.2 Linux基础知识
> 1. **ls** 
> **查看**目录
> 
> 2. **cd**  xx
> **切换**到xx目录，目录不存在会报错，且可以是 路径+文件夹
> 
> 3. **cp** -r /usr/tmp /opt
> **复制** /usr/tmp目录 到 /opt目录下面
> 
> 4. **mv**  -r /usr/tmp /opt
> ***移动*** /usr/tmp目录 到 /opt目录下面
> 
> 5. **rm** -rf xx
> **删除**xx文件或者文件夹，慎用
> 
> 6. **mkdir** tools
> **创建**tools名称文件夹在当前目录下
> 
> 7. **touch** cj.py
> **创建** cj.py文件在当前目录下
>
>8. **pwd**
>**路径**打印

## 2 Installation
### 2.0 重要提示
> ### ***！！！除了自定义安装其余的不需要部署代码！！！***
> i : interactive 代表交互
> -t : tty 分配伪 TTY
> [关于-it和-d](https://www.jb51.net/server/28596066e.htm)

### 2.1 最省心最省时间配置-docker安装
> 拉取镜像
> > docker pull chenjunnn/rm_vision:lastest
> 
> 构建开发容器
> > docker run -d --privileged --network host \
-v ws:/ros_ws --name rv_devel \
chenjunnn/rm_vision:lastest \
tail -f /dev/null
> 
>
>>docker run -it \
--privileged --network host \
-v /home/arffy/Project/vision_ws:/ros_ws \
-v /dev:/dev -v $HOME/.ros:/root/.ros \
--name rv_devel codrobot:v4 \
ros2 launch foxglove_bridge foxglove_bridge_launch.xml
>
> 构建运行容器
> > docker run -it --privileged --network host \
-v ws:/ros_ws --restart always --name rv_runtime \
chenjunnn/rm_vision:lastest \
/bin/bash -c "source /ros_ws/install/setup.bash &&
ros2 launch rm_vision_bringup vision_bringup.launch.py camera_type:=hik"

### 2.2 省心最省时间配置-tar包安装
> 使用tar包镜像安装
> > 快管群里的小伙伴要tar包
> > > 待更新humble包
> > > > <a href="#锚点1">安装docker</a>	
> > > >
> > > > > 加载tar包

### 2.3 有点省心省时间配置-dockerfile安装
- 0. click_right	<u>打开终端</u>
- 1. sudo apt update	<u>更新源</u>
- 2. sudo apt install python3-pip	<u>安装pip，安装py包</u>
- 3. sudo apt install git	<u>安装git，拉取仓库</u>
- 4. git clone --branch 1 --depth 1 https://github.com/chenjunnn/rm_vision.git 	<u>拉取最新分支镜像仓库</u>
- 5. <a href="#锚点1">安装docker</a>
- 6. cd rm_vision	<u>进入镜像仓库</u>
- 7. docker build -t vision:v3 .	<u>编译镜像</u>


### 2.4 不太省心省时间配置-自定义安装
- 0. click_right	<u>打开终端</u>
- 1. sudo apt update	<u>更新源</u>
- 2. sudo apt install python3-pip	<u>安装pip，安装py包</u>
- 3. sudo apt install git	<u>安装git，拉取仓库</u>
- 4. wget http://fishros.com/install -O fishros && . fishros 	<u>如果使用docker的话，可以选择**11.一键ros+docker安装**，看情况自由选择，最后会让你输入名字，此名字是你以后docker容器的名字，此处使用仅作中介，可随意输入，这里输入 zero 。另外能安装什么版本ros，和你的ubuntu内核有关</u>
- 5. zero (enter) e (enter) e (enter) <u>这样就可以进入中介的容器了</u>
- 6、exit  <u>退出容器</u>

## 3 Docker
### 3.0 docker安装
- wget http://fishros.com/install -O fishros && . fishros 	<span name = "锚点1"><u>选择**8.一键docker安装**</u></span>

### 3.1 docker基本使用
> 1. **docker version** 
> **版本**信息
> 
> 2. **docker ps**  -l -a
> **列出容器**-l:运行的 | -a:所有的
> 
> 3. **docker start** zero
> **启动容器** zero 
> 
> 4. **docker stop** zero
> ***停止容器*** zero 
> 
> 5. **docker rm** zero
> **删除容器**zero ，容器状态必须停止
> 
> 6. **docker** images
> **列出镜像**
> 
> 7. **docker rmi** images_name
> **删除镜像** images_name,容器状态必须停止
>
> 8. **docker build**
> **构建容器**使用Dockerfile
>
> 9. **docker run**
> ** 创建运行容器**
>
> 10. **docker exec**
> ** 在运行的容器中执行命令**
>
> 11. **docker logs**
> ** 查看容器日志**
>
> 12. **docker commit** [OPTIONS:-a -m] CONTAINER [REPOSITORY[:TAG]]
> **打成镜像** -a:新镜像作者 -m:提交说明
>
> 13. **docker save** [OPTIONS:-o] IMAGE [IMAGE...]
> **打包镜像** -o:指定输出文件
>
> 14. **docker load** [OPTIONS:-i -q]
> **载入镜像** -i:用于指定载入镜像的文件 -q:精简输出信息
>
> 15. **docker system prune -af --volumes** 清理缓存垃圾
>
> 16. **docker rename <container_id> <new_name>** 更改容器名字
>
> 15. **docker export -o container.tar [container_id]** 导出容器的文件的更改文件系统
>
> 16. **docker import container.tar new_image_tag** 将导出的文件系统导入为一个新的镜像

## 4 Configuration
### 4.0 无docker环境配置
- 1. gedit ~/.bashrc	<u>在末尾添加下列语句，`<distro>`为ros版本</u>
- 2. source /opt/ros/` <distro> `/setup.bash	<u>加载环境</u>
- 3. ros2 	<u>在终端输入ros，有回显证明安装完毕</u>

### 4.1 有docker环境配置
#### 4.1.0 <span name = "锚点2">配置自定义容器</span>
##### 4.1.0.0 一般使用这个，解决一切问题
> #### docker run -it --name robot -v /home/cod:/home/cod --privileged=true --net=host  -e DISPLAY=:0 -v /dev:/dev codrobot:v1
> 
> robot为容器名字	
> /cod为你的用户名	
> codrobot:v1为镜像+标签名字	

##### 4.1.0.1 附加选项
> #### -p 9000:9000 --gpus all -e NVIDIA_DRIVER_CAPABILITIES=compute,utility
> 
> -p 9000:9000某些软件需要端口映射，无--net=host时使用		
> --gpus -e	此处则是对GPU的支持，无GPU不可用

> #### -e DISPLAY=:0 -v /tmp/.X11-unix:/tmp/.X11-unix
> 
> 设置环境变量及转发参数

#### 4.1.1 环境配置
> ### 目前手动引入，写进  .bashrc 里会导致冲突不能生效
> 可以写入/etc/bash.bashrc

### 4.2 镜像制作及使用
- 1. sudo docker ps -a	查看robot容器编号eg: eda05ad514f8
- 2. sudo docker commit -a "ArFFy" -m "create new img" eda05ad514f8 codrobot:v0	命令以容器为基础生成镜像codrobot:v0
- 3. sudo docker image ls	查看镜像是否生成
- 4. sudo docker save -o codrobot:v0.tar codrobot:v0	镜像打包为 tar 文件
- 5. sudo docker load -i codrobot:v0.tar	换设备，重新载入镜像

### 4.3 调试代码

#### 4.3.0 部署代码

- 1. cd Desktop/	进入桌面
- 2. mkdir ros2_ws	创建工作区
- 3. cd ros2_ws 	进入工作区
- 4. mkdir src 		  创建src
- 5. cd src			进入src
- 4. &emsp;git clone --branch 1 --depth 1 https://github.com/chenjunnn/rm_vision.git
- 5. &emsp;git clone --branch 1 --depth 1 https://github.com/chenjunnn/rm_auto_aim.git 
- 6. &emsp;git clone --branch 1 --depth 1 https://github.com/nolem-77/ros2_hik_camera.git 
- 7. &emsp;git clone --branch 1 --depth 1 https://github.com/chenjunnn/rm_gimbal_description.git 
- 8. &emsp;git clone --branch 1 --depth 1 https://github.com/chenjunnn/rm_serial_driver.git 

#### 4.3.1 创建并运行容器

- <a href="#锚点2">去创建运行环境</a>
- **docker exec -it robot bash**	可以在终端进去运行状态的容器

#### 4.3.2 试错编译

- 1. cd ros2_ws	进入工作区
- 2. source /opt/ros/humble/setup.bash	引入ros2环境变量
- 3. colcon build	<a href="#锚点3">可能会出错，请查询最后一节</a>
- 4. source install/setup.bash	引入程序环境变量
- 5. ros2 launch rm_vision_bringup vision_bringup.launch.py	执行程序

> ###### 图像可视化方式
- -  rqt->Plugins->image view
- -  rviz2->topic
- -  foxglove-studio

## 5 visualization
### 5.0 X11转发
> ### 容器外
- 1. ifconfig                          ##假设为xxx.xxx.xxx.xx
- 2. echo $DISPLAY   (要在显示屏查看，其他ssh终端不行)  ##假设为:0
- 3. sudo apt install x11-xserver-utils	安装xserver
- 4. sudo vim /etc/lightdm/lightdm.conf 	增加许可网络连接
- 5. xserver-allow-tcp=true	在末尾添加
- 6. sudo systemctl restart lightdm	重启
- 7. xhost +	给予权限
> ### 容器内
- export DISPLAY=xxx.xxx.xxx.xx:0	可以写入/etc/bash.bashrc
> ### 验证
- sudo apt-get install xarclock
- xarclock	看到时钟图即为安装成功

> ##  [MobaXterm](https://mobaxterm.mobatek.net/)
> sudo dpkg -i <path_to_downloaded_file.deb> 安装
> docker run -itd --privileged --network host -v /home/arffy/Project/vision_ws:/ros_ws -v /dev:/dev -v $HOME/.ros:/root/.ros -e DISPLAY=$DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix --name test codrobot:v6 bash

> ## wsl.con
> ### 容器外
> sudo apt-get install xfce4 xterm
> export DISPLAY=localhost:0.0
> export DISPLAY=$(cat /etc/resolv.conf | grep nameserver | awk '{print $2}'):0.0    检查DISPLAY环境变量
> xhost +local:    允许WSL访问X服务器

### 5.1 foxglove
#### 5.1.0安装
- https://foxglove.dev/download	下载适合安装包
- sudo apt install ./foxglove-studio-*.deb
- sudo apt update && sudo apt install foxglove-studio
- foxglove-studio	终端输入就能打开

#### 5.1.1使用Rosbridge连接
> ### 容器内
- sudo apt install ros-humble-rosbridge-suite 
- ros2 launch rosbridge_server rosbridge_websocket_launch.xml
> ### 容器外
- foxglove-studio->Rosbridge

## 6 Adaptation

### 6.0 贴上图标
![不要白嫖](https://raw.githubusercontent.com/chenjunnn/rm_vision/daf06676d5de9f4eaac291ab01d661323cb76c82/docs/rm_vision.svg)

### 6.1 调节相机参数

> ##### exposure_time:2000-5000 曝光时间是指传感器的采样频率，也就是每秒钟采集多少张图像。曝光时间越短，图像越清晰，但亮度会降低。曝光时间越长，图像越亮，但会出现拖影或模糊的现象。

> ##### gain:8-n 增益是指对图像信号进行放大的程度，也就是提高图像的亮度。增益越高，感光越灵敏，图像亮度越高，但噪点也会被放大。增益越低，噪点越少，但图像可能过暗或细节丢失。

> ### 如何调节曝光时间和增益，主要取决于你的拍摄环境和目标效果。一般来说，有以下几个建议：
> 1. 亮度充足的场景下可以适当降低曝光时间和增益，改善拖影和过曝的问题。
> 2. 亮度不足的场景下可以适当提高曝光时间和增益，提升图像亮度和细节。
> 3. 有强点光源的场景下可以适当降低增益，抑制点光源过曝。
> 4. 运动场景下可以适当降低曝光时间和增益。

> #### detect_color 检测的颜色0-蓝  1-红

> #### min_lightness 灯条二值化阈值

> #### classifier_threshold 识别器阈值

> #### ignore_classes 跳过检测种类

### 6.2 标定相机
==***待补充ing***==

### 6.3 调节卡尔曼参数

==***待补充ing***==

### 6.10 自启动脚本

==***待补充ing***==

## 6 Simulator
==***待补充ing***==

## 7 Other
### 7.1 HelloWorld
- 1. 创建功能包
> ros2 pkg create 包名 --build-type 构建类型 --dependencies 依赖列表 --node-name 可执行程序名称
>> --build-type：是指功能包的构建类型，有cmake、ament_cmake、ament_python三种类型可选；
>> --dependencies：所依赖的功能包列表；
>> --node-name：可执行程序的名称，会自动生成对应的源文件并生成配置文件。
>> ros2 pkg create pkg01_helloworld_cpp --build-type ament_cmake --dependencies rclcpp --node-name helloworld
>> ros2 pkg create pkg02_helloworld_py --build-type ament_python --dependencies rclpy --node-name helloworld

- 2. 编译&引用环境
> colcon build
>> colcon build --packages-select 功能包列表
> . install/setup.bash
>> echo "source /home/.../install/setup.bash" >> ~/.bashrc
> ros2 run pkg01_helloworld_cpp helloworld

- 3. 查找
> ros2 pkg executables[包名]#输出所有功能包或指定包下的可执行程序
> ros2 pkg list#列出所有功能包
> ros2 pkg prefix 包名#列出功能包路径
> ros2 pkg xml #输出功能包的packge.xml内容

- 4. 执行
> ros2 run 功能包 可执行程序 参数

## 8 <span name = "锚点3">Supplement</span>
- 1. 安装docker失败
> <font color=red size=5>Get permission denied while trying to connect</font>
>
> > 1. grep docker /etc/group	检查用户组
> > 2. sudo usermod -aG docker $USER	组添加用户
> > 3. newgrp docker	生效
> > 4. groups 	检查成员

- 2. 获得GPU的计算支持
> <font color=red size=5>docker: Error response from daemon: could not select device driver ““ with capabilities: [[gpu]]</font>
>
> <https://blog.csdn.net/u013685264/article/details/123206768?ops_request_misc=&request_id=&biz_id=102&utm_term=docker:%20Error%20response%20from%20da&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduweb~default-0-123206768.142^v86^insert_down1,239^v2^insert_chatgpt&spm=1018.2226.3001.4187>
>
> > 添加nvidia-docker的源
> > > 1. curl -s -L https://nvidia.github.io/nvidia-docker/gpgkey | \
> sudo apt-key add -
> distribution=$(. /etc/os-release;echo $ID$VERSION_ID)
> > > 2. curl -s -L https://nvidia.github.io/nvidia-docker/$distribution/nvidia-docker.list | \
  sudo tee /etc/apt/sources.list.d/nvidia-docker.list
> > > 3. sudo apt-get update
> > 
> > 安装nvidia-container-toolkit
> > > sudo apt-get install -y nvidia-container-toolkit
> > 
> > 重启docker
> > > sudo systemctl restart docker

- 3. image_transport.hpp|
- 	cv_bridge.h|
- 	camera_info_manager.hpp|
- 	angles.h
> <font color=red size=5>fatal error:image_transport/image_transport.hpp:No such file or directory</font>
> > sudo apt-get install ros-humble-image-transport
> 
> <font color=red size=5>fatal error: cv_breidge/cv_bridge.h:No such file or directory</font>
> > sudo apt-get install ros-<distro>-cv-bridge
> 
> <font color=red size=5>fatalerror:camera_info_manager/camera_info_manager.hpp:No such file or directory</font>
> > sudo apt-get install ros-noetic-camera-info-manager
> 
> <font color=red size=5>fatal error:angles/angles.h:No such file or directory</font>
> > sudo apt-get install ros-<distro>-angles
>


- 3. OpenCV
```
CMake Error at CMakeLists.txt:20 (find_package):
  By not providing "FindOpenCV.cmake" in CMAKE_MODULE_PATH this project has
  asked CMake to find a package configuration file provided by "OpenCV", but
  CMake did not find one.

  Could not find a package configuration file provided by "OpenCV" with any
  of the following names:

    OpenCVConfig.cmake
    opencv-config.cmake

  Add the installation prefix of "OpenCV" to CMAKE_PREFIX_PATH or set
  "OpenCV_DIR" to a directory containing one of the above files.  If "OpenCV"
  provides a separate development package or SDK, be sure it has been
  installed.
```
> >sudo apt-get install libopencv-dev