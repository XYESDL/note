# CAN通讯

## OBDⅡ
![接口定义](/OBD.png)

## 开发板 
[乐鑫官网](https://www.espressif.com.cn/zh-hans)

![ESP32C3-GPIO](/esp32c3.png)

[ESP32C3规格书](https://www.espressif.com/sites/default/files/documentation/esp32-c3_datasheet_cn.pdf)

## 开发工具
[Arduino](https://www.arduino.cc/)

[Arduino库](https://docs.arduino.cc/libraries/)

[MicroPython](https://www.micropython.org/)

## CAN三方库
[CAN库](https://github.com/sandeepmistry/arduino-CAN)

[ESP32-CAN监听固件](https://github.com/collin80/ESP32RET)

## API
[OpenDBC Python API](https://github.com/commaai/opendbc)

## CAN数据分析工具
[采集分析SavvyCAN](https://www.savvycan.com/)

[obd2-pid-table](https://www.csselectronics.com/pages/obd2-pid-table-on-board-diagnostics-j1979)

[开源DBC库](https://github.com/commaai/opendbc)

## ESP32 CAN项目
[MrDIY](https://mrdiyca.gitlab.io/mrdiy-esp-online-flasher/)

[MrDIY-store](https://store.mrdiy.ca/)

[ESP32 CAN项目](https://mc.dfrobot.com.cn/thread-317271-1-1.html)

[ESP32RET](https://github.com/collin80/ESP32RET)


## 论坛
[Arduino社区](https://arduino.me/home)

[合宙文档](https://wiki.luatos.com/chips/esp32c3/board.html)

## 配件

CAN收发器芯片-SN65HVD231DR  Rx = GPIO4、Tx = GPIO5

LDO（低压差线性稳压器）-AMS1117

## OBD-CAN屏项目流程

### CAN抓包

- 硬件：ESP32、CAN收发器
- 固件：ESP32RET
- 软件：SavvyCAN

### 通讯

- 硬件：ESP32C3、CAN收发器、圆屏
- 库：CAN