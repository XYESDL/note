# 软硬件平台

[嘉立创](https://www.jlc.com/)、
[嘉立创EDA](https://lceda.cn/)、
[嘉立创开源平台](https://oshwhub.com/)

## 硬件

[B站视频1](https://space.bilibili.com/395188578)、
[B站视频2](https://space.bilibili.com/43584648)、

### MOS管

[MOS视频](https://www.bilibili.com/video/BV17y421B7D7?spm_id_from=333.788.videopod.sections&vd_source=e809ebb6871d94b76c8a649bc323c48d)

振铃效应、米勒平台、推挽、图腾柱
```vue
寄生
栅极串联电阻
RC缓冲电路
```
### 晶振

```vue



```


## 工具

电烙铁
```vue
T12、C245
```
### 点焊机

ESP32 C3、RMT、MOS驱动IC

```vue
双脉冲点焊：
t1（预焊脉冲）：单次高电流短脉冲（去氧化）
t2（间隔）：零电流
t3（主焊脉冲）：单次高电流长脉冲（熔核形成）
```

```vue
MOS管发热不均：电流分配不均、优化对称走线、降低阻抗
栅极振荡（振铃）：寄生电感过大、增加栅极电阻、缩短走线
开关速度不一致：栅极驱动信号延迟不同、采用星型走线、独立驱动
EMI噪声大：大电流环路面积过大、使用多层板、减小环路面积
TVS二极管：跨接在MOSFET的D-S极（如30V钳位）、贴近MOSFET(感性负载关断,产生反向电动势)
```

```vue
D-S电阻：确保可靠关断，选10kΩ。
G-S电阻：控制开关速度，选1Ω~100Ω。
G-S二极管：加速关断并保护栅极（快恢复或肖特基型）-米勒效应
```


https://www.ti.com/cn/lit/ds/symlink/ucc21520.pdf?ts=1758497911272




### 手机直供电

[示例1](https://www.youtube.com/watch?v=7f8SliNGeDM)
[示例2](https://www.bilibili.com/video/BV1LmjhzzEEw/?spm_id_from=333.337.search-card.all.click&vd_source=e809ebb6871d94b76c8a649bc323c48d)

iphone改造过程

```vue
- 使用稳压模块(纹波)给电池保护板提供4.2V、3A电流，开机过程大电流跳动 或使用二极管(MUR460)正向压降0.7V，5V到4.3V，防止电流倒灌
- 开机时会检测电池电压，用于开机电量显示
- 可装法拉电容用于峰值电流需求
```

```vue
USB不供电保留数据通讯：VBUS(断开) │ D+ │ D- │ GND 
插电开机：CC/ID引脚：识别电源类型，并唤醒PMIC
```