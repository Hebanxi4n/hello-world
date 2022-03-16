机器人在进行路径规划时，通过gmapping扫描来构建一张环境全局地图，但是这张环境全局地图是静态的，只包含黑白灰三种像素，黑色表示无法通行区域，白色表示可以自由移动区域，灰色表示未知区域。可以设想，当机器人在这种环境下规划路径是不安全的，因为我们无法实时更新地图，导致机器人“看”不到新出现的障碍物。同时，如果在规划移动路径时，机器人与障碍物贴的过近，很有可能出现碰撞或者卡顿，因此我们需要让机器人和障碍物（也即黑色区域）保持一定的距离。
![image](https://github.com/Hebanxi4n/hello-world/blob/aa78096140af2ecc10b617deef759c6d9e0200f8/images/1531712385705504.png)

costmap在ROS中通过功能包costmap_2d来实现，costmap_2d包括local_costmap(为局部路径规划而准备)和global_costmap(为全局路径规划而准备)。这两者都可以配置多个图层。

-Static Map Layer:静态地图层，基本上不变的地图层，是通过slam扫描得到的。

-Obstacle Map Layer:障碍物地图层，这是动态的地图层，它会实时更新传感器感知到的障碍物信息。

-Inflation Layer:膨胀层，将以上两张地图进行膨胀，防止机器人在运动中撞到障碍物。

-Other Layer:你可以通过插件形式自己实现costmap。

我们可以通过move_base内部逻辑流程图来
![image](https://github.com/Hebanxi4n/hello-world/blob/ff4980e27b4173b9efbac0e2e014a8bdd88238e1/images/1531722258772314.png)
