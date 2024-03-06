# GameFormer_Planner复现记录

## 一、环境配置
### 1、下载nuplan数据集
### 2、下载nuPlan_devkit(v1.2.2)
### 3、下载代码并配置开发依赖
```shell
git clone https://github.com/MCZhi/GameFormer-Planner.git && cd GameFormer-Planner

conda create -n nuplan python=3.8
conda activate nuplan
pip install -r requirements.txt

# 激活环境变量
export NUPLAN_EXP_ROOT="$HOME/nuplan/exp"
```

## 二、操作步骤
### 1、数据处理
```shell
# 前提要下载好nuplan数据
python data_process.py \
--data_path nuplan/dataset/nuplan-v1.1/splits/mini \
--map_path nuplan/dataset/maps \
--save_path nuplan/processed_data
```

### 2、训练
```shell
# train_set 处理好的训练集路径
# valid_set 处理好的验证集路径
python train_predictor.py \
--train_set nuplan/processed_data/train \
--valid_set nuplan/processed_data/valid
```

### 3、测试
```shell
# data_path 数据
# map_path 地图
# model_path 模型
python run_nuplan_test.py \
--experiment_name open_loop_boxes \
--data_path nuplan/dataset/nuplan-v1.1/splits/mini \
--map_path nuplan/dataset/maps \
--model_path training_log/your/model
```