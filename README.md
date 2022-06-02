# 根据fishros和ros2文档学习

# 配置vscode python和cpp 智能分析包，智能代码检测
```bash
"python.analysis.extraPaths": ["./install/village_interfaces/lib/python3.8/site-packages"]
```

# 1 建包
cpp
```bash
cpp ros2 pkg create --build-type ament_cmake --node-name my_node my_package --dependencies rclcpp std_msgs
```

python
```bash
cpp ros2 pkg create --build-type ament_python --node-name my_node my_package --dependencies rclcpp std_msgs
```

注意接口的使用

# 2 chapter4 小说插图话题建立和订阅，并显示图像，李四发布 王二订阅显示cpp

```c++
1 在li4中添加发布小说的话题，其中msg为Novel接口
  替换所有msg 的 string为Novel接口
3 在wang2中增加process_image函数，创建指向msg->image的指针，传入
    auto msg_img_ptr = std::make_shared<sensor_msgs::msg::Image>(msg->image);
    process_image(msg_img_ptr,true);

```
# 3 chapter5 parameter和action, 目的，
李四写小说的速度 参数
参数是节点的一个配置值，
名字：李四写小说周期，值：5s
名字：显示器亮度,值：60%
```python
bool 和bool[]，布尔类型用来表示开关，比如我们可以控制雷达控制节点，开始扫描和停止扫描。
int64 和int64[]，整形表示一个数字，含义可以自己来定义，这里我们可以用来表示李四节点写小说的周期值
float64 和float64[]，浮点型，可以表示小数类型的参数值
string 和string[]，字符串，可以用来表示雷达控制节点中真实雷达的ip地址
byte[]，字节数组，这个可以用来表示图片，点云数据等信息
```

命令:设置、保存、恢复
```bash
ros2 param set /turtlesim background_b 122
ros2 param dump /turtlesim

ros2 run turtlesim turtlesim_node
ros2 param load  /turtlesim ./turtlesim.yaml

启动节点时添加
ros2 run <package_name> <executable_name> --ros-args --params-file <file_name>
ros2 run turtlesim turtlesim_node --ros-args --params-file ./turtlesim.yaml

```

## python参数更改写作周期

rclpy.node.Node内置功能

函数名称	描述
declare_parameter	声明和初始化一个参数
declare_parameters	声明和初始化一堆参数
get_parameter	通过参数名字获取一个参数
get_parameters	通过多个参数名字获取多个参数
set_parameters	设置一组参数的值
更多函数	Node — rclpy 0.6.1 documentation (ros2.org)


```python

# 声明参数,参数名字，默认值
self.declare_parameter("write_timer_period",5)

timer的回调函数里
# 回调之后更新回调周期
timer_period = self.get_parameter('write_timer_period').get_parameter_value().integer_value
# 更新回调周期
self.timer.timer_period_ns = timer_period * (1000*1000*1000)

```
查看主题发布速度
ros2 topic hz /sexy_girl

# git pull test