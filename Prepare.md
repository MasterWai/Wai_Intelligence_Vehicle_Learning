# ROS（ROS1）需求环境：Ubuntu 18.04 / 20.04（30系显卡）

# 安装Ubuntu的准备：
1. 打开磁盘管理，选剩余空间大的硬盘，右键压缩卷，大小至少25G（单位是M，G*1024=M）以上，之后会有未分配的空间，进入下一步。没有25G的话，你好，已经结束了。
2. 准备U盘（16G或以上）
3. 下载rufus（http://rufus.ie/downloads/），建议portable
4. 下载Ubuntu镜像（https://releases.ubuntu.com/?_ga=2.127430925.1873823062.1667755070-1084943650.1667755070），
   选择对应版本 18.04 / 20.04，下载Desktop image
5. 打开rufus，设备选择U盘，引导类型选镜像文件，右边选刚刚下载的镜像，剩下全部默认，点击开始，等待完成。
6. 重启，进BIOS（搜自己电脑品牌看是按哪个键），手速很快但进不去的话，在windows系统下关闭快速启动，再重试。
7. 关闭安全启动。
8. 调整Boot顺序，U盘放第一，或者直接引导进U盘。

# 安装Ubuntu的过程：
1. 引导进U盘后，选择Ubuntu install（18.04）或者Ubuntu（20.04）。
2. 进入Ubuntu后，按提示进行安装。
3. 硬盘位置多选正常安装，少则最小安装（最好不要，因为会缺少扫雷和纸牌接龙，下载安装ROS的时候很无聊）。
4. 选择其他选项
5. 分区环节，因为刚刚windows分了空间出来，选择未分配的空间，点击+，逻辑分区，开始位置，efi，1024M。
6. 选择剩余的未分配空间，点击+，主分区，开始位置，EXT4，挂载点\，大小拉满。
7. 安装启动引导器的设备选择刚刚新建的efi分区的编号（不要选错windows的windows boot manager）。
8. 剩余自己喜欢怎么选就怎么选。
9. 等待安装，完毕后，重启，拔u盘。
10.重启后，界面（紫色背景，名叫GRUB）应该有Ubuntu和Windows boot manager，选Ubuntu

# 进入Ubuntu后的配置及显卡安装：
1. 更换清华源
2. 打开终端（ctrl+alt+T）
2. sudo passwd
3. sudo apt update
4. sudo apt upgrade
5. 显卡驱动？。。
# 安装ROS（18.04，melodic）
1. 打开终端（ctrl+alt+T）
2. 添加软件源：sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
3. 设置密钥：sudo apt-key adv --keyserver 'hkp://keyserver.ubuntu.com:80' --recv-key C1CF6E31E6BADE8868B172B4F42ED6FBAB17C654
4. 检查软件源更新：sudo apt update
5. 安装ros：sudo apt install ros-melodic-desktop-full，过程很慢，甚至可能失败，多试几次（可以边扫雷边等）。
6. 初始化ros：sudo rosdep init
7. 升级ros组件：rosdep update**
8. 添加ros的环境变量到系统的bash中：echo "source /opt/ros/melodic/setup.bash" >> ~/.bashrc
9. 刷新环境变量：source ~/.bashrc
10. 安装依赖：sudo apt-get install python-rosinstall python-rosinstall-generator python-wstool build-essential

# 安装ROS（20.04，noetic）
1. 打开终端（ctrl+alt+T）
2. 添加软件源：sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
3. 设置密钥：sudo apt-key adv --keyserver 'hkp://keyserver.ubuntu.com:80' --recv-key C1CF6E31E6BADE8868B172B4F42ED6FBAB17C654
4. 检查软件源更新：sudo apt update
5. 安装ros：sudo apt install ros-noetic-desktop-full
6. 添加ros的环境变量到系统的bash中：echo "source /opt/ros/noetic/setup.bash" >> ~/.bashrc
7. 刷新环境变量：source ~/.bashrc

# 小海龟测试
0. 开3个终端
1. roscore
2. rosrun turtlesim turtlesim_node
2.1 没有该包->sudo apt-get install ros-$(rosversion -d)-turtlesim 
    #$(rosversion -d)可直接替换为你安装的ros版本代号，如noetic...<p>
3. rosrun turtlesim turtle_teleop_key
