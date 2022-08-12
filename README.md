## 简介

本项目结合 VSCode 的 Remote - Containers 插件搭建 PHP 开发环境，安装应用有 PHP、Nginx默认安装版本如下。  

| 应用  | 版本                     |
| ----- | ------------------------ |
| PHP   | 7.4                      |
| Nginx | 1.20(默认安装最新稳定版) |

可选安装 node 和 yarn，在容器启动后执行 `docker-app -i node` 或 `docker-app -i yarn` 安装。

## 环境搭建

首先需要安装 Docker 如果是 windows 系统的话可以安装 wsl2 并在 wsl2 中安装 Docker。  
其次 VSCode 需要安装 remote-containers 插件。  

### 开始使用

注意：该项目容器默认会添加到 database_app 网络，如果 database_app 网络不存在则会无法构建，解决方法如：  
1. 删除 `.devcontainer\devcontainer.json` 配置文件中 `runArgs` 配置项的 `--network=database_app` 即可。  
2. 添加 database_app 网络，添加命令 `docker network create database_app`。另可以部署一个数据库 [docker-database 项目](https://github.com/xueyong-q/docker-database.git)。  

nginx 配置，项目配置文件在 `.devcontainer/nginx/` 目录下的 Adefault.conf 文件中。nginx 的日志文件则在 `.devcontainer/nginx/log` 目录中。   

首先使用 VSCode 打开本项目，操作如下。  
![](.devcontainer/image/image-1.jpg)

然后选择在容器中重新打开。  
![](.devcontainer/image/image-2.jpg)

最后等待项目启动，项目启动后会将容器中的 81 端口映射到主机的 80 端口。 

如要修改端口映射，可以修改 `.devcontainer\devcontainer.json` 配置文件中 `appPort` 配置项。  
构建 Dockerfile 时的环境变量则在 `build.args` 中修改。  

另已安装的 xdebug 扩展默认的端口是 9001，如需修改端口则在 `.devcontainer/php/conf.d/xdebug.ini` 配置文件的 `xdebug.remote_port` 选项修改。  

## VSCode 扩展

| 扩展名称                   | 描述 |
| -------------------------- | ---- |
| PHP Intelephense           |      |
| PHP Debug                  |      |