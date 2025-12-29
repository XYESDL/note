# 中控品牌及控制协议

串口模块：有人、中盛科技

类型：HEX(十六进制0-9、A-F)、ASCLL

[shutown on lan](https://github.com/ford77/SOL)

[展厅相关软件](https://www.tree666.com/)

## 品牌

### [AMX](https://www.amx.com/zh)

系统编程软件[NetLinx Studio](https://www.amx.com/zh/products/netlinx-studio)

```vue
PROGRAM_NAME='HJ'
DEFINE_DEVICE

IPad		=10001:1:0
Power_a     =5001:1:0
Power_v		=0:3:0
Switch_a	=5001:2:0

DEFINE_CONSTANT
DEFINE_TYPE
DEFINE_VARIABLE
DEFINE_LATCHING
DEFINE_MUTUALLY_EXCLUSIVE

([IPad,10]..[IPad,12])
([IPad,20],[IPad,21])

DEFINE_START

IP_CLIENT_OPEN(Power_v.port, '192.168.0.7', 8000, IP_UDP)

DEFINE_EVENT
data_event[Power_a]{online:{send_command Power_a,'SET BAUD 2400,N,8,1 485 ENABLE'}}
data_event[Switch_a]{online:{send_command Switch_a,'SET BAUD 115200,N,8,1 485 DISABLE'}}
button_event[IPad,0]
    {
	push:
	    {
	    select
		{
		active(button.input.channel=10): {on[IPad,10]}
		active(button.input.channel=11): {on[IPad,11]}
		active(button.input.channel=12): {on[IPad,12]}
		}
	    }
    }
button_event[IPad,20]{hold[20]:{
				on[IPad,20]
				on[IPad,22]
				send_string Power_a,"$55,$01,$00,$0D,$F0,$AA"
				wait 10
				on[IPad,24]
				send_string Power_v,"$40,$30,$30,$46,$41,$30,$30,$30,$30,$30,$30,$30,$30,$30,$30,$31,$30,$32,$42,$31,$30,$30,$30,$30,$30,$30,$30,$30,$30,$32,$30,$30,$30,$31,$46,$46,$46,$46,$30,$34,$2A,$0D"
				}}
button_event[IPad,22]{hold[20]:{
				on[IPad,22]
				send_string Power_a,"$55,$01,$00,$0D,$F0,$AA"
				}}
button_event[IPad,30]{push:{send_string Switch_a,"'Level1 increment level 1 0.5',$0D,$0A"}}

DEFINE_PROGRAM
```

触控面板设计/编程[TPDesign](https://www.amx.com/products/TPDesign5/)

![图片](/tpdesign.png)

面板上传软件[TPTransfer](https://support.touchpanelcontrol.com/support/solutions/articles/19000078645-tptransfer-download-link)

终端软件[TPControl](https://store.touchpanelcontrol.com/tpcontrol/)

[视频教程](https://www.bilibili.com/video/BV1BG4y1t7T2/?spm_id_from=333.337.search-card.all.click&vd_source=e809ebb6871d94b76c8a649bc323c48d)

### VANCSYS

[软件](http://ctl.vancsys.com/)

```vue
IDE-HControll
APP-HPanel
```
新建设备-选择驱动包-指定接口

![1](/ws1.png)

UI设计-定义按钮事件

![2](/ws2.png)

### CREATOR快捷

UI--ThinkDraw--[注册地址拼接](http://thinkdraw.ty.ff255.cn/manageSystem/thinkdraw/register?)

编辑软件--ThinkControl

### AVSYS

### 淳中

### SONY

```vue
VISCA OVER IP
通过UDP协议进行控制，端口号是52381

命令格式如下： 01  00  00  09  00  00  00  01  8X  01  06  01  VV  WW  03  01  FF
（X表示摄像头的编号，VV上下的速度，WW表示左右的速度<0-18>16进制）
表示16进制， 8X前的代码为封装包，其中的 09表示后面控制代码的位数。最后一个 01为计数，每发完一条命令之后，需要重新发送一条清空命令才能继续发送命令，否则发送的命令无效。
清空命令是： 02  00  00  01  00  00  00  00  01。

上 01 00 00 09 00 00 00 01 81 01 06 01 18 17 03 01 FF
下 01 00 00 09 00 00 00 01 81 01 06 01 18 17 03 02 FF
左 01 00 00 09 00 00 00 01 81 01 06 01 18 17 01 03 FF
右 01 00 00 09 00 00 00 01 81 01 06 01 18 17 02 03 FF
停 01 00 00 09 00 00 00 01 81 01 06 01 18 18 03 03 FF

预置位存储：01 00 00 07 00 00 00 01 8X 01 04 3F 01 0P FF（X表示摄像机地址位，P表示预置位号<0-15>）

1号预置位存储：01 00 00 07 00 00 00 01 81 01 04 3F 01 00 FF
1号预置位调用：01 00 00 07 00 00 00 01 81 01 04 3F 02 00 FF

2号预置位存储：01 00 00 07 00 00 00 01 81 01 04 3F 01 01 FF
2号预置位调用：01 00 00 07 00 00 00 01 81 01 04 3F 02 01 FF

3号预置位存储：01 00 00 07 00 00 00 01 81 01 04 3F 01 02 FF
3号预置位调用：01 00 00 07 00 00 00 01 81 01 04 3F 02 02 FF

焦距近：      01 00 00 06 00 00 00 01 81 01 04 07 34 FF
停止：        01 00 00 06 00 00 00 01 81 01 04 07 00 FF

焦距远：      01 00 00 06 00 00 00 01 81 01 04 07 24 FF
停止：        01 00 00 06 00 00 00 01 81 01 04 07 00 FF
```

## 常用协议

### RS232

| 引脚 | 定义 | 说明 |
| :---: | :----: | :---: |
| 2 | RXD  | 接收数据 |
| 3 | TXD  | 发送数据 |
| 5 | GND  | 接地 |

### RS422

| 差分电路 | 四线全双工 |
| :----: | :---: |
| RT+ | TR+ |
| RT- | TR- |

### RS485


### TCP、UDP

### IR

