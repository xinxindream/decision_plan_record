# Ros学习记录
## 一些问题
1. Marker.mesh_resource方法
```python
# mesh_resource需要用url进行赋值
# http://, ftp://, package:// file://
url = ""
marker.mesh_resource = url
```

## 一些函数
1. rospy.Timer()
```python
'''
parameters:
    1. period: 一个 rospy.Duration 对象，表示定时器触发的时间间隔。
    2. callback: 当定时器触发时调用的函数。这个函数接收一个 TimerEvent 对象作为参数，该对象包含有关定时器的信息（例如，上一次和当前的触发时间，以及从期望的触发时间开始的延迟）。
    3. oneshot (可选): 如果设置为 True，定时器将只触发一次，然后自动停止。默认为 False，表示定时器将持续触发，直到它被显式停止。

functions:
    用于创建定时器。定时器会在指定的时间间隔后调用一个回调函数。这对于定期执行某些任务（例如，定期发布消息或检查某些条件）非常有用。
'''
```
2. rospy.Duration()
```python
'''
parameters:
    time: secs || nsecs 

functions:
    用于表示一段时间。常用于处理时间戳、等待一段时间、或设置定时器等。
'''
```
3. rospy.Rate()
```python
'''
parameters:
    rate: xxHz, 表示循环的频率，单位是“次每秒”或“赫兹”

functions:
    用于控制循环的执行频率。通常配合sleep函数，在循环中使用
'''
```
4. rospy.spin()
```python
'''
parameters:
    none

functions:
    用于阻止当前线程，直到ROS节点被关闭。换句话说，它使得你的程序保持运行，直到节点被关闭或者ROS被关闭。
'''
```