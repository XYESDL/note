## Debian开启root ssh登录

```vue
PermitRootLogin yes
PasswordAuthentication yes
```

运维面板
[1Panel](https://1panel.cn/)、[宝塔](https://www.bt.cn/new/index.html)

## 视频流

### [SRS](https://ossrs.net/lts/zh-cn/)+[WebRTC](https://webrtc.org/?hl=zh-cn)

RTMP->SRS服务器->WEBRTC网页

#### [Jitsi Meet](https://github.com/jitsi/jitsi-meet)

[教程1](https://post.smzdm.com/p/akle006k/)、[教程2](https://blog.laoda.de/archives/docker-compose-install-jitsi)

内网使用

```vue
- 配置内网DNS域名解析
- Nginx负载均衡
- 浏览器限制单域名连接数，多域名均衡
- 自签SSl证书（强制使用HTTPS）
```