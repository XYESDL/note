## 常用命令

- sudo netstat -tulpn | grep :8000 查看端口占用

## 工具

### Docker

- docker images 查看本地镜像
- docker pull <镜像名:标签> 拉取镜像
- docker rmi <镜像名或ID> 删除镜像
- docker rmi -f <镜像名或ID> 强制删除镜像
- docker network ls 查看网络列表
- docker start <容器名或ID> 启动容器
- docker stop <容器名或ID> 停止容器
- docker restart <容器名或ID> 重启容器
- docker ps 查看运行中的容器
- docker ps -a 查看所有容器（包括停止的）

### 运维面板
[1Panel](https://1panel.cn/)、[宝塔](https://www.bt.cn/new/index.html)

### 视频流

[SRS](https://ossrs.net/lts/zh-cn/)+[WebRTC](https://webrtc.org/?hl=zh-cn)

RTMP->SRS服务器->WEBRTC网页

[Jitsi Meet](https://github.com/jitsi/jitsi-meet)

[教程1](https://post.smzdm.com/p/akle006k/)、[教程2](https://blog.laoda.de/archives/docker-compose-install-jitsi)

### 开源考试系统

[xmky-exam](http://www.xiaomaokaiyuan.com/open-products)

### GitHub

GitHub Pages

```vue
new repository --> Settings--> Pages --> Build and deployment --> GitHub Actions
```

源代码管理

```vue
设置身份
    git config --global user.name "***"
    git config --global user.email "***"
删除现有的 origin
    git remote remove origin
查看远程仓库列表
    git remote -v
设置系统代理
    git config --global http.proxy http://127.0.0.1:7890
    git config --global https.proxy http://127.0.0.1:7890

git clone    #克隆
git pull origin main --rebase  # 同步更新
git status  #当前状态
git init    #初始化
git add .   #添加到缓存区
git commit -m "feat: 初始化项目"    #提交代码
git branch -M main    #选择分支
git remote add origin https://github.com/user/repo.git    #连接远程仓库（首次）
git push -u origin main    #推送

```