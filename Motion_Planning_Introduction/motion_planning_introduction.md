# 运动规划综述（Motion Planning）

## 一、什么是运动规划

运动规划（Motion Planning）指车辆在**一定约束**下从起点到终点的**几何**路径，同时给出车辆沿该路径运动的速度信息。  
运动规划（Motion Planning）以**最优性**为核心，在环境中给定起点和终点的条件下，规划机器人**无冲突行进**的状态序列。运动规划框架如下所示，主要包含路径规划与轨迹规划两大组件。
![运动规划](../运动规划.png "motion_planning")


### 1.1 约束

1. 交通规则
2. 运动学约束

> 不能实现瞬时侧向移动，前驱的车辆必须依赖前轮的转向才能实现变道、转向等操作，在弯道上不能速度过快等等

1. 静态障碍物(Static Obstacle)约束

> 静态障碍物(Static Obstacle)是道路上静止的车辆、路面中间的石墩子等车辆不可行驶的区域（全局规划考虑）

1. 动态障碍物约束

> 实时处理行人、车辆等各种运动的障碍物，避免与障碍物发生碰撞事故 （局部规划考虑）

### 1.2 路径规划（Path Planning）
1. 路径规划以可达性为核心，基于几何约束（如静态障碍物，地图等），规划机器人首末位置间无冲突行进的最优路径（路径长度尽量短）序列。   
2. 这样的最优路径序列，在二维空间表现为可行驶的几何曲线，这样的集合曲线由一系列路径点（waypoints）构成，路径点是空间中的位置或关节角度
3. 路径规划只有几何属性，不考虑时间序列信息，一般用在全局规划
![路径规划](../image.png "motion_planning")

### 1.3 轨迹规划（Trajectory Planning）
1. 轨迹规划以稳定性和快速性为核心，基于运动学、动力学约束和路径序列，规划实时运动状态（位置，朝向，速度以及加速度等）以逼近全局路径。
2. 轨迹规划在路径规划的最优路径序列的基础上，为其加上时间序列信息。所以其输入为全局路径、动态环境和模型约束，通常在局部范围内进行动态避障和路径跟踪。

## 二、传统运动规划
传统运动规划主要有两种轨迹生成，一种是直接生成轨迹法，一种是路径-速度分解法。以Apollo为代表
### 2.1 路径规划 && 速度规划
在实际工程应用中，下发的往往是路径而非轨迹，这意味着轨迹规划被分解为路径规划 + 速度规划的两阶段计算架构，即首先生成行驶的几何曲线，随后考虑以何种速度沿着规划的曲线行驶。采用该种方式原因总结如下  
（1）轨迹规划计算过程困难，这种分解方式能大幅度降低求解难度。   
（2）通过规划生成的轨迹，本身就难以在后续控制模块中被有效的跟踪。   
（3）决策规划模块仅需生成路径而非轨迹，车辆实际运动速度暂时无法或无需决策。

### 常见算法
1. 基于采样（RRT，PRM）
2. 基于图搜索（A*, Dijstra）
3. 最优控制法（MPC）

## 三、端到端运动规划
端到端的方法通常采用深度学习或者深度强化学习进行。end to end方法输入到输出的映射有两种，一种是输入图像等感知信息输到出方向盘转角等控制量，另一个是感知信息到车模的状态量，如速度、坐标等，二者均需要大量的数据做支撑。以GameFormer为代表

## 四、优缺点


## 五、评价标准
1. 舒适度和路径平滑程度相关
