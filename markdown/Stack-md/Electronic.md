# 软硬件

[B站视频1](https://space.bilibili.com/395188578)、
[B站视频2](https://space.bilibili.com/43584648)

## PCB

[嘉立创](https://www.jlc.com/)、
[嘉立创EDA](https://lceda.cn/)、
[嘉立创开源平台](https://oshwhub.com/)

## MOS驱动电路（点焊机）

![nmos](/ucc51520.png)

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

### OBDⅡ
![接口定义](/OBD.png)

### CAN三方库
[CAN库](https://github.com/sandeepmistry/arduino-CAN)

[ESP32-CAN监听固件](https://github.com/collin80/ESP32RET)

### API
[OpenDBC Python API](https://github.com/commaai/opendbc)

### CAN数据分析工具
[采集分析SavvyCAN](https://www.savvycan.com/)

[obd2-pid-table](https://www.csselectronics.com/pages/obd2-pid-table-on-board-diagnostics-j1979)

[开源DBC库](https://github.com/commaai/opendbc)

### ESP32 CAN项目
[MrDIY](https://mrdiyca.gitlab.io/mrdiy-esp-online-flasher/)

[MrDIY-store](https://store.mrdiy.ca/)

[ESP32 CAN项目](https://mc.dfrobot.com.cn/thread-317271-1-1.html)

[ESP32RET](https://github.com/collin80/ESP32RET)

### 配件

CAN收发器芯片-SN65HVD231DR  Rx = GPIO4、Tx = GPIO5

LDO（低压差线性稳压器）-AMS1117

### CAN抓包

- 硬件：ESP32、CAN收发器
- 固件：ESP32RET
- 软件：SavvyCAN

## 工具

[JBC245电烙铁](https://oshwhub.com/search?wd=JBC245)

## 杂项

### 手机直供电

[示例1](https://www.youtube.com/watch?v=7f8SliNGeDM)

[示例2](https://www.bilibili.com/video/BV1LmjhzzEEw/?spm_id_from=333.337.search-card.all.click&vd_source=e809ebb6871d94b76c8a649bc323c48d)