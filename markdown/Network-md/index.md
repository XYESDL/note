# 网络

## 模拟软件

ENSP、[PNETLab](https://pnetlab.com/pages/main)

192.168.10.1/24

常见CIDR表示法
|CIDR|子网掩码|可用IP数量|
|:----:|:---:|:---:|
|/24|255.255.255.0|254|
|/25|255.255.255.128|126|
|/26|255.255.255.192|62|
|/30|255.255.255.252|2|

|VLAN作用|影响|
|:----|:---|
|减少广播域	|降低广播风暴风险，提高网络效率|
|提升安全性	|默认不同 VLAN 不能互通，可用 ACL 控制访问|
|便于管理	|设备按部门/用途划分，配置更清晰|
|灵活部署	|设备不受物理位置限制，随时加入合适的 VLAN|
|可控的互通	|通过三层交换机路由，受控跨 VLAN 访问|

|模式|支持VLAN|数据包处理方式|应用场景
|:----|:---|:---|:---|
|Access|一个VLAN|不带VLAN标签|连接PC、服务器等终端设备
|Trunk|多个VLAN|都带VLAN标签（除 Native VLAN）|交换机间互联、连接路由器
|Hybrid|多个VLAN|可以选择是否带VLAN标签|适用于AP、IP电话等设备

## 交换机

```vue
查看设备型号和版本信息、运行时间、系统时间
display version、device、clock

查看所有接口的简要状态、vlanif、统计信息
display interface brief、vlanif、g 0/0/1、counters

查看所有VLAN、VLAN 10、接口所属的VLAN信息
display vlan、vlan 10、port vlan

查看MAC地址表、动态学习的MAC地址、指定VLAN的MAC地址
display mac-address、mac-address dynamic、mac-address vlan 10

查看静态路由、OSPF路由、IP路由表、ARP表、指定IP的ARP信息
display ip routing-table protocol static、ospf routing、ip routing-table、arp、arp 192.168.1.1

查看系统日志、告警信息、CPU使用率、内存使用率、历史CPU使用率
display logbuffer、trapbuffer、diagnostic-information、cpu-usage、memory-usage、cpu-usage history

查看生成树协议（STP）状态、ACL规则、指定ACL的详细信息
display stp、acl all、acl 2001

查看指定端口的STP信息（如GigabitEthernet 0/0/1）
display stp interface GigabitEthernet 0/0/1

查看DHCP服务器状态、DHCP地址池信息
display dhcp server statistics、dhcp pool

查看已保存的配置、当前运行的配置
display saved-configuration、current-configuration

查看设备温度、电源状态、风扇状态、保存当前配置、重启交换机
display temperature、power、fan、save、reboot
```

```vue
登录交换机并进入系统视图
[Huawei] system-view

进入需要配置的接口视图。配置接口GigabitEthernet 0/0/1：
[Huawei] interface GigabitEthernet 0/0/1
[Huawei-GigabitEthernet0/0/1]

为接口配置IP地址（通常用于管理接口或三层接口）：
[Huawei-GigabitEthernet0/0/1] ip address 192.168.1.1 255.255.255.0

启用或禁用接口
[Huawei-GigabitEthernet0/0/1] undo shutdown\shutdown

设置速率为100Mbps，双工模式为全双工：
[Huawei-GigabitEthernet0/0/1] speed 100
[Huawei-GigabitEthernet0/0/1] duplex full
恢复为自动协商：
[Huawei-GigabitEthernet0/0/1] undo speed
[Huawei-GigabitEthernet0/0/1] undo duplex

为接口添加描述信息，便于管理：
[Huawei-GigabitEthernet0/0/1] description "Link to Server"

将接口加入VLAN 10（Access模式）：
[Huawei-GigabitEthernet0/0/1] port link-type access
[Huawei-GigabitEthernet0/0/1] port default vlan 10

将接口设置为Trunk模式，并允许VLAN 10通过：
[Huawei-GigabitEthernet0/0/1] port link-type trunk
[Huawei-GigabitEthernet0/0/1] port trunk allow-pass vlan 10

修改接口的MTU值（默认为1500字节）：
[Huawei-GigabitEthernet0/0/1] mtu 1600

启用接口的流量控制功能：
[Huawei-GigabitEthernet0/0/1] flow-control

查看当前接口的配置信息：
[Huawei-GigabitEthernet0/0/1] display this

配置完成后，保存配置：
[Huawei] save

退出接口视图，返回系统视图：
[Huawei-GigabitEthernet0/0/1] quit

查看接口状态：
[Huawei] display interface GigabitEthernet 0/0/1

查看接口简要信息：
[Huawei] display interface brief

接口模式：根据需求选择Access、Trunk或Hybrid模式。

IP地址配置：只有三层接口（如VLAN接口或路由接口）才需要配置IP地址。

保存配置：配置完成后务必使用save命令保存，否则重启后配置会丢失
```

```vue
创建VLAN、批量创建VLAN、删除VLAN
[Huawei] vlan 10、vlan batch 10 20 30、undo vlan 10
[Huawei-vlan10] quit

三层交换与VLAN间路由
创建VLAN接口并配置IP地址：
[Huawei] interface Vlanif 10
[Huawei-Vlanif10] ip address 192.168.10.1 255.255.255.0
[Huawei-Vlanif10] quit

启用三层交换功能：
[Huawei] ip routing

添加静态路由：
[Huawei] ip route-static 192.168.2.0 255.255.255.0 192.168.1.1
删除静态路由：
[Huawei] undo ip route-static 192.168.2.0 255.255.255.0 192.168.1.1

动态路由协议
启用OSPF：
[Huawei] ospf 1
[Huawei-ospf-1] area 0
[Huawei-ospf-1-area-0.0.0.0] network 192.168.1.0 0.0.0.255
启用RIP：
[Huawei] rip 1
[Huawei-rip-1] network 192.168.1.0

端口绑定MAC地址
port-security mac-address命令用来配置Sticky-Config类型的静态安全MAC地址。
undo port-security mac-address命令用来删除Sticky-Config类型的静态安全MAC地址。

链路聚合（Eth-Trunk）
创建Eth-Trunk：
[Huawei] interface Eth-Trunk 1
将接口加入Eth-Trunk：
[Huawei] interface GigabitEthernet 0/0/1
[Huawei-GigabitEthernet0/0/1] eth-trunk 1
[Huawei-GigabitEthernet0/0/1] quit

启用STP：
[Huawei] stp enable

配置STP模式（如MSTP）
[Huawei] stp mode mstp

查看STP状态：
[Huawei] display stp

创建基本ACL：
[Huawei] acl 2001
[Huawei-acl-basic-2001] rule permit source 192.168.1.0 0.0.0.255
[Huawei-acl-basic-2001] quit

应用ACL到接口：
[Huawei] interface GigabitEthernet 0/0/1
[Huawei-GigabitEthernet0/0/1] traffic-filter inbound acl 2001

创建流量分类：
[Huawei] traffic classifier c1
[Huawei-classifier-c1] if-match acl 2001
[Huawei-classifier-c1] quit

创建流量行为：
[Huawei] traffic behavior b1
[Huawei-behavior-b1] remark dscp af11
[Huawei-behavior-b1] quit

创建QoS策略并应用：
[Huawei] traffic policy p1
[Huawei-trafficpolicy-p1] classifier c1 behavior b1
[Huawei-trafficpolicy-p1] quit
[Huawei] interface GigabitEthernet 0/0/1
[Huawei-GigabitEthernet0/0/1] traffic-policy p1 inbound

启用DHCP服务器：
[Huawei] dhcp enable

创建DHCP地址池：
[Huawei] ip pool pool1
[Huawei-ip-pool-pool1] network 192.168.1.0 mask 255.255.255.0
[Huawei-ip-pool-pool1] gateway-list 192.168.1.1
[Huawei-ip-pool-pool1] quit

在接口上启用DHCP：
[Huawei] interface Vlanif 10
[Huawei-Vlanif10] dhcp select global

启用端口安全：
[Huawei] interface GigabitEthernet 0/0/1
[Huawei-GigabitEthernet0/0/1] port-security enable

限制MAC地址数量：
[Huawei-GigabitEthernet0/0/1] port-security max-mac-num 5

启用SNMP：
[Huawei] snmp-agent

配置SNMP团体名：
[Huawei] snmp-agent community read public
[Huawei] snmp-agent community write private

配置日志主机：
[Huawei] info-center loghost 192.168.1.100

设置日志级别：
[Huawei] info-center source default channel loghost log level informational

配置Telnet登录：
[Huawei] user-interface vty 0 4
[Huawei-ui-vty0-4] authentication-mode password
[Huawei-ui-vty0-4] set authentication password cipher Huawei@123
[Huawei-ui-vty0-4] user privilege level 15

配置SSH登录：
[Huawei] stelnet server enable
[Huawei] rsa local-key-pair create
[Huawei] user-interface vty 0 4
[Huawei-ui-vty0-4] authentication-mode aaa
[Huawei-ui-vty0-4] protocol inbound ssh

```

access接口类型。
通过端口组批量将接口加入VLAN

```vue
[HUAWEI] port-group pg1  //创建端口组pg1
[HUAWEI-port-group-pg1] group-member gigabitethernet1/0/1 to gigabitethernet1/0/5
[HUAWEI-port-group-pg1] port link-type access
[HUAWEI-port-group-pg1] port default vlan 10

[HUAWEI] vlan 10
[HUAWEI-vlan10] port gigabitethernet 1/0/1 to 1/0/5
```
### 实例

![vlan](/switch.png)

```vue
PC1 属于 VLAN 10，IP 地址：192.168.10.1/24，网关：192.168.10.254
PC2 属于 VLAN 20，IP 地址：192.168.20.1/24，网关：192.168.20.254
SW2A 是二层交换机，负责连接 PC1 和 PC2
SW3A 是三层交换机，负责 VLAN 10 和 VLAN 20 之间的路由
SW2A 通过 trunk 口连接 SW3A，承载 VLAN 10 和 VLAN 20 的数据流量

配置 SW2A（二层交换机）
创建 VLAN 并配置端口
[SW2A] system-view
[SW2A] vlan batch 10 20

配置 PC1 和 PC2 所连接的端口为 Access 端口
[SW2A] interface Ethernet 0/0/1
[SW2A-Ethernet0/0/1] port link-type access
[SW2A-Ethernet0/0/1] port default vlan 10

[SW2A] interface Ethernet 0/0/12
[SW2A-Ethernet0/0/12] port link-type access
[SW2A-Ethernet0/0/12] port default vlan 20
[SW2A-Ethernet0/0/12] quit

配置连接 SW3A（三层交换机）的端口为 Trunk
[SW2A] interface GigabitEthernet 0/0/1
[SW2A-GigabitEthernet0/0/1] port link-type trunk
[SW2A-GigabitEthernet0/0/1] port trunk allow-pass vlan 10 20
[SW2A-GigabitEthernet0/0/1] quit

配置 SW3A（三层交换机）
创建 VLAN
[SW3A] system-view
[SW3A] vlan batch 10 20

配置 VLAN 接口（SVI）
[SW3A] interface Vlanif10
[SW3A-Vlanif10] ip address 192.168.10.254 255.255.255.0

[SW3A] interface Vlanif20
[SW3A-Vlanif20] ip address 192.168.20.254 255.255.255.0

配置 Trunk 端口，允许 VLAN 10 和 VLAN 20 通过
[SW3A] interface GigabitEthernet 0/0/1
[SW3A-GigabitEthernet0/0/1] port link-type trunk
[SW3A-GigabitEthernet0/0/1] port trunk allow-pass vlan 10 20
[SW3A-GigabitEthernet0/0/1] quit
确保三层交换机启用 IP 路由
```

## 防火墙 


## 软路由

[ikuai](https://www.ikuai8.com/component/download)

[x-wrt](https://x-wrt.com/)

[openwrt_x86_x64](https://github.com/DHDAXCW/OpenWRT_x86_x64?tab=readme-ov-file)

## 光猫

超级管理员账号密码获取、桥接[参考图文](https://www.bilibili.com/opus/907251136224821285?spm_id_from=333.999.0.0)

## VPN

|  |  | 
| :---- | :--- |
| android | [ClashMeta](https://github.com/MetaCubeX/ClashMetaForAndroid) |
| ios/mac | [shadowrocket](https://www.shadowrocket.vip/) |
|windows、linux|[Clash](https://www.clashforwindows.net/clash-for-windows-download/)|