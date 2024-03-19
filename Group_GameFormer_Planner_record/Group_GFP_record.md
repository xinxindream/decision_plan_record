# 组内决策规划代码--rosbag to nuplan流程
## 一、相关文件
```shell
# 数据处理文件
xiaoba_rosbag_tonuplan.py

# 训练
train_predictor-plantf-1211.py

# 测试
xiaoba_rosbag_test.py

# 可视化
rviz -d xiaoba_rosbag_test.rviz

# car.dae
~/workspace/hjj/ws_perception
```

# 一、数据处理
## 1、数据路径
```shell
# 总体路径
/data/dataset/xiaoba

# rosbag路径
/data/dataset/xiaoba/2024.1.11

# 车道线数据
/data/dataset/xiaoba/lane_route_line

# 处理结果（用来做训练集）保存路径
/data/dataset/xiaoba/2024.1.11/xxx_train/
```

## 2、调试中间数据
### 2.1 rosbag数据
```python
path:        /data/datasets/xiaoba/2024.1.11/2024-01-11-17-20-37_part1_with_det_2.bag
version:     2.0
duration:    10:49s (649s)
start:       Jan 12 2024 11:13:52.53 (1705029232.53)
end:         Jan 12 2024 11:24:42.46 (1705029882.46)
size:        30.1 GB
messages:    300719
compression: none [14569/14569 chunks]
types:       apollo_message_pkg/DriverGnssBestPose                
             apollo_message_pkg/DriverGnssLocalizationEstimate    
             apollo_message_pkg/DriverGnssLocalizationEstimateNew 
             autoware_lanelet2_msgs/MapBin                        
             autoware_msgs/DetectedObjectArray
             kxdun_localization_msgs/Localization                 
             kxdun_perception_msgs/PerceptionLaneArray            
             kxdun_perception_msgs/PerceptionObstacleArray        
             kxdun_perception_msgs/RSObjectArray                  
             nav_msgs/Path                                     
             sensor_msgs/Image                                    
             sensor_msgs/PointCloud2                              
             visualization_msgs/MarkerArray                       
topics:      /bev/pose                         64986 msgs @ 99.7 Hz : apollo_message_pkg/DriverGnssLocalizationEstimateNew
             /bevfusion_objects                 6439 msgs @  9.9 Hz : kxdun_perception_msgs/RSObjectArray                 
             /border3dpts_bev0                  8097 msgs @ 12.9 Hz : nav_msgs/Path                                       
             /border3dpts_bev1                  8097 msgs @ 12.9 Hz : nav_msgs/Path                                       
             /border3dpts_bev2                  8097 msgs @ 12.9 Hz : nav_msgs/Path                                       
             /border3dpts_bev3                  8097 msgs @ 12.9 Hz : nav_msgs/Path                                       
             /concat_lidar_bevfusion            6442 msgs @  9.9 Hz : sensor_msgs/PointCloud2                             
             /det3dpts_bev0                     8099 msgs @ 12.9 Hz : nav_msgs/Path                                       
             /det3dpts_bev1                     8099 msgs @ 12.9 Hz : nav_msgs/Path                                       
             /det3dpts_bev2                     8097 msgs @ 12.9 Hz : nav_msgs/Path                                       
             /kxdun/ego_vehicle/localization   64987 msgs @ 99.6 Hz : kxdun_localization_msgs/Localization                
             /kxdun/perception/lanes            8101 msgs @ 12.9 Hz : kxdun_perception_msgs/PerceptionLaneArray           
             /kxdun/perception/obstacles        6439 msgs @  9.9 Hz : kxdun_perception_msgs/PerceptionObstacleArray       
             /localization_pose_ros            64986 msgs @ 99.6 Hz : apollo_message_pkg/DriverGnssLocalizationEstimate   
             /objects                           6439 msgs @  9.9 Hz : autoware_msgs/DetectedObjectArray                   
             /objects_markers                   6439 msgs @  9.9 Hz : visualization_msgs/MarkerArray                      
             /ph/sensor/gnss/best_pose           650 msgs @  1.0 Hz : apollo_message_pkg/DriverGnssBestPose               
             /vector_map                           1 msg            : autoware_lanelet2_msgs/MapBin                       
             /vector_map_marker                    1 msg            : visualization_msgs/MarkerArray                      
             /zkhy_stereo/left/color            8126 msgs @ 12.5 Hz : sensor_msgs/Image

options = {'compression': 'none', 'chunk_threshold': 786432}
siez = 32351633590
```

### 2.2 route_line_location数据
> ./csv_data

### 2.3 agent_list
```
id: 1
    position: 
      x: -44.139306603836246
      y: -154.61593601935726
      z: 38.93623014359247
    heading: -0.0891343755943474
    velocity: 0.0
    length: 4.085164147667251
    width: 1.5517751593080633
    vel_heading: -0.0891343755943474...
```

# 模型训练测试
## 1、模型训练
### 1.1 训练文件
TODO: 模型修改解析
> train_predictor-plantf-1211.py

### 1.2 参数
```shell
--name
"Exp3"
--train_set
/data/datasets/xiaoba/2024.1.11/2024-01-11-17-20-37_part1_with_det_2_train/train
--valid_set
/data/datasets/xiaoba/2024.1.11/2024-01-11-17-20-37_part1_with_det_2_train/valid
```

## 2、模型测试
### 2.1 测试文件
> xiaoba_rosbag_test.py

### 2.2 rviz文件
在测试文件执行后，运行rviz
> rviz -d xxx.rviz