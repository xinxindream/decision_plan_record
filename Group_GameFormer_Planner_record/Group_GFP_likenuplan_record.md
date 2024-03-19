# 针对likenuplan流程
## 一、相关文件
```shell
# 数据处理文件
xiaoba_rosbag_tonuplan_likenuplan.py

# 训练
train_predictor.py

# 测试
run_nuplan_test.py
```

## 二、操作流程
### 1、数据处理
1. 修改 xiaoba_rosbag_tonuplan_likenuplan.py
    - 修改rosbag路径
    - 修改save_path路径
    - 修改self._original_route_lane_data_x_path & self._shifit_route_lane_data_x_path，当然还有y轴的

2. 运行就行，如果是pycharm则配置好环境，terminal则conda activate nuplan

3. 数据处理保存目录
```shell
# train
/data/datasets/xiaoba/2024.1.11/2024-01-11-17-20-37_part2_with_det_2_train/train/

# valid
/data/datasets/xiaoba/2024.1.11/2024-01-11-17-20-37_part2_with_det_2_train/valid/
```

4. 数据分析
dim=2, 特征为50, 符合GameFormerPlanner源码

### 2、训练模型
