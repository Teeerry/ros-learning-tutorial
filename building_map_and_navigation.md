# 定位和导航
SLAM(simultaneous localization and mapping) 即同时定位和导航

准确的定位需要精确的地图,精确的地图需要准确的定位.
## 通过传感器数据构建地图
建图的目的是实现自主导航,构建结果产生两个包含地图信息的文件:map_name.pgm map_name.yaml
地图构建过程主要是根据scan,tf等主题,使用 gmapping 包的 slam_gmapping 节点建图:
1. 通过bag文件进行建图(bag能够多次利用,构建出更合适的地图,推荐使用!!!)
2. 直接使用主题信息进行构图

## 机器人自主导航
机器人自主导航需要解决两个问题:它现在在哪里和它要去哪里,即分别对应(定位和导航)
### 定位
我们可以通过 amcl(Adaptive Monte Carlo Localization) 包里面的算法实现机器人的定位.机器人初始位置的获取对导航非常重要,精确的导航需要依靠准确的定位.
### 导航
navigation system(nav stack) 是ROS移动机器人中应用广泛的移动导航系统.它的工作流程大概分为四步:
1. 发送 navigation goal 到 nav stack.
2. nav stack 使用 global planner 规划到达目标的最短轨迹.
3. 规划好的轨迹被发送到 local planner, local planner 按照接受到的轨迹移动同时负责整合传感器信息和实现避障,如果无法继续移动则回到第二步,使用 global planner 重新规划.
4. 当机器人距离目标位姿足够近时,停止运动.