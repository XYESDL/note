## 电路知识

[博客-基础知识讲解](https://thiscute.world/posts/electrical-engineering-circuits-basics-1/#back-to-top)

[B站视频1](https://space.bilibili.com/395188578)

[B站视频2](https://space.bilibili.com/43584648)

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