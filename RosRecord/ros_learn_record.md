# Ros学习记录
## 一些问题
1. Marker.mesh_resource方法
```python
# mesh_resource需要用url进行赋值
# http://, ftp://, package:// file://
url = ""
marker.mesh_resource = url
```