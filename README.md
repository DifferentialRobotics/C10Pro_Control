## C10Pro_Control
本项目基于UDP协议发送角度控制指令给云卓C10Pro云台，以实现通过命令行对云台角度进行控制。 \
云台说明书详见：[C10_C10PRO产品说明书](C10_C10PRO产品说明书.pdf) \
云台控制协议详见：[云卓云台相机协议v1.1.5](云卓云台相机协议v1.1.5.pdf)

## 使用步骤
1.首先检查云台与无人机是否正常连接，云台网口默认IP为192.168.144.108，使用ping命令检查连接：
```
  ping 192.168.144.108
```

2.克隆本项目至自己的工作空间并运行角度控制脚本：
```
  git clone https://github.com/DifferentialRobotics/C10Pro_Control.git
  cd C10Pro_Control
  python angel_control.py
```

根据脚本输出的提示选择需要控制的轴后输入期望角度即可。目前支持yaw角和pitch角控制，以及一键回中。

3.本项目还提供了发送用户自定义控制指令脚本[custom_control.py](custom_control.py)，并提供了几种控制指令示例：
```
  MODE_NORMAL_CMD = "#TPUG2wPTZ0A7B"  #吊装模式命令
  MODE_REVERSE_CMD = "#TPUG2wPTZ0B7C" #倒装模式命令
  UP_CMD = "#TPUG2wPTZ016BE3"         #一键朝上看命令
  DOWN_CMD = "#TPUG2wPTZ026CE5"       #一键朝下看命令
```
其通过调用 **send_custom_command** 接口将指令报文发送给云台：

```
  controller.send_custom_command(MODE_NORMAL_CMD)
```
用户可以使用示例指命令或根据[云卓云台相机协议v1.1.5](云卓云台相机协议v1.1.5.pdf)自定义控制指令，将其传至 **send_custom_command** 接口中，并运行该脚本发送指令：
```
  python custom_control.py
```