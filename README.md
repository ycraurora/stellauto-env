# stellauto
StellaAutonomous System 脚本工具

## 用法
使用git下载脚本至本地
```
git clone https://github.com/ycraurora/stellauto.git
```

### Ubuntu配置脚本(WIP)

### docker配置脚本
- Windows
1. 于官网中下载docker desktop安装文件并安装；
2. 下载ycrad/stellauto:latest镜像，并创建容器；
3. 使用vscode, WSL2, dev container连接容器。
- Ubuntu
1. 在docker文件夹中存在两个shell脚本文件，其中install_docker.sh用于安装并配置docker，startup.sh用于拉取镜像并启动容器：
```
sudo chmod a+x install_docker.sh
./install_docker.sh
xhost +
sudo chmod a+x startup.sh
./startup.sh
```
2. 使用vscode与dev container插件连接镜像即可。
- 注意
若在vscode中使用clangd，需要将clangd path设置为`/usr/bin/clangd`。

## TCP/UDP连接
### Windows部署client与docker
在Windows系统下同时部署client与docker，可直接通过docker容器ip连接client与server。
### Windows部署client，宿主机(ubuntu)部署docker
在Windows系统下部署client，在宿主机(ubuntu)中部署docker，通过以下方式连接client与server：
1. 获取docker容器ip (DOCKER_IP)，于docker容器命令行键入命令，获取ip，例如：172.17.0.2：
```
echo $(hostname -I | awk '{print $1}')
```
2. 获取宿主机ip (HOST_IP)，例如：192.168.1.3；
3. 于Windows中打开'终端管理员'，添加经由HOST_IP转发的路由：
```
route add -p 172.17.0.0 mask 255.255.0.0 192.168.1.3
```
4. 于宿主机中关闭防火墙:
```
sudo ufw disable
```
5. 于Windows中通过ping测试：
```
ping 172.17.0.2
```
