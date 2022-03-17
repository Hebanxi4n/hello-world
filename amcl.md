### amcl
amcl接收基于激光的地图、激光扫描、变换信息，输出位置估计。在一开始，amcl根据提供的参数初始化它的粒子滤波器。
值得注意的是，如果没有预设参数，在默认地情况下，初始滤波器将是以(0,0,0)为中心的粒子云。

#### 订阅的话题
scan(**sensor_msgs/LaserScan**)
>激光扫描

tf(**tf/tfMessage**)
>坐标变换

initialpose (**geometry_msgs/PoseWithCovarianceStamped**)
>用于初始化粒子滤波器的均值和方差

map (**nav_msgs/OccupancyGrid**)
>当设置了use_map_topic参数时，AMCL会订阅这个话题来检索基于激光定位的地图（navigation 1.4.2中的新内容)

#### 发布的话题
amcl_pose (**geometry_msgs/PoseWithCovarianceStamped**)
>机器人在地图中的pose估计和协方差

particlecloud (**geometry_msgs/PoseArray**)
>由滤波器维护的姿态估计集合

