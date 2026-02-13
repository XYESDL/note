# 软硬件

[B站视频1](https://space.bilibili.com/395188578)、
[B站视频2](https://space.bilibili.com/43584648)

## PCB

[嘉立创](https://www.jlc.com/)、
[嘉立创EDA](https://lceda.cn/)、
[嘉立创开源平台](https://oshwhub.com/)

## MOS驱动电路（点焊机）

![nmos](/ucc21520.png)

开：MCU方波 -- 驱动芯片 -- 10Ω均流电阻MOS G

关：GS电容 -- 10K泄放电阻、关断二极管 -- 驱动芯片GND

[MOS电路](https://www.bilibili.com/video/BV17y421B7D7?spm_id_from=333.788.videopod.sections&vd_source=e809ebb6871d94b76c8a649bc323c48d)

[ucc21520驱动芯片](https://www.ti.com/cn/lit/ds/symlink/ucc21520.pdf?ts=1758497911272)

```vue
双脉冲点焊：

预焊脉冲：高电流短脉冲（去氧化）

间隔

主焊脉冲：高电流长脉冲（熔核形成）
```

```vue

栅极振荡：寄生电感过大、增加栅极电阻1Ω~100Ω、缩短走线

开关速度不一致：栅极驱动信号延迟不同、采用星型走线、独立驱动

TVS二极管：感性负载关断,产生反向电动势，接在MOSFET的D-S极

地隔离：光耦+驱动芯片、隔离芯片

D-S电阻：确保可靠关断，选10kΩ。

G-S二极管：加速关断并保护栅极（快恢复或肖特基型）-米勒效应
```

## CAN通讯

开源适配器[CANable 2](https://canable.io/)

[ESP32-CAN](https://github.com/collin80/ESP32RET)

### 上位机软件
[SavvyCAN](https://www.savvycan.com/)

[CANgaroo](https://github.com/Schildkroet/CANgaroo)

### 协议

物理层CAN2 A、CAN2 B、CAN FD

通讯层SLCAN、SocketCAN、GVRET

## OBDⅡ
![接口定义](/OBD.png)

### DBC库
[OpenDBC Python API](https://github.com/commaai/opendbc)

### OBD2-PID
[obd2-pid-table](https://www.csselectronics.com/pages/obd2-pid-table-on-board-diagnostics-j1979)

### ESP32 CAN项目
[MrDIY](https://gitlab.com/MrDIYca/canabus)

[MrDIY-store](https://store.mrdiy.ca/)

[ESP32 CAN项目](https://mc.dfrobot.com.cn/thread-317271-1-1.html)

### 配件

CAN收发器芯片-SN65HVD23X

LDO（低压差线性稳压器）-AMS1117

## 工具

[JBC245电烙铁](https://oshwhub.com/search?wd=JBC245)

### 手机直供电

[示例1](https://www.youtube.com/watch?v=7f8SliNGeDM)

[示例2](https://www.bilibili.com/video/BV1LmjhzzEEw/?spm_id_from=333.337.search-card.all.click&vd_source=e809ebb6871d94b76c8a649bc323c48d)