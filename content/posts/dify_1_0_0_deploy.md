+++
date = '2025-02-28T23:24:28+08:00'
title = 'Dify 1.0.0 podman部署'

draft = false
tags = ["docker", "podman", "dify"]
categories = ["docker", "podman", "dify"]
featuredImagePreview = "https://img.picui.cn/free/2025/03/01/67c1ecbc5e45c.png"
+++

# Dify 1.0.0 docker部署
> dify今天发布了1.0.0版本, 在公司玩dify玩的不亦乐乎，手痒难耐，今天在家也部署一下，正好aliyun白嫖的100w token, 接进来玩玩。

## 部署环境
- 系统：ubuntu24.04
- podman: 4.9.3

## 前置条件
- podman已经配置好了可用源
- podman-docker、podman-compose已经安装, podman-docker可以让你使用docker命令来操作podman，没装的话可以用`apt-get install podman-docker` `apt-get install podman-compose`安装，podman-compose可以让你使用docker-compose文件

## 部署步骤
```shell
# 克隆项目
git clone https://github.com/langgenius/dify.git --branch 1.0.0
# 进入项目docker目录
cd dify/docker
# 复制.env.example文件为.env，这里需要注意， docker部署默认用了80和443端口，
# 如果你的其他docker服务 也在使用，需要修改.env文件中的端口映射，如下：
# ------------------------------
# Docker Compose Service Expose Host Port Configurations
# ------------------------------
# EXPOSE_NGINX_PORT=8886
# EXPOSE_NGINX_SSL_PORT=8443
cp .env.example .env
# 拉取镜像，时间可能较长，耐心等待
docker compose up -d
# 检查服务状态
docker compose ps
```
## 启动
{{< admonition type=tip title="提示" open=true >}}
- 如果你部署的并非1.0.0版本, 则需要改一下nginx的配置文件，否则就会遇到卡install界面的问题，解决方案看[这里](https://blog.csdn.net/qq_53597256/article/details/143745465)
{{< /admonition >}}

- 打开浏览器，输入`http://你的服务器地址:8886/install`，进入dify的安装界面，按照提示安装即可
- 设置好管理员账号密码，就能愉快的玩耍了

## 尾注
- 到这里dify的docker部署就算是完成了，过程很简单，如果有问题，看官网文档 [https://docs.dify.ai/zh-hans/getting-started/install-self-hosted/docker-compose](https://docs.dify.ai/zh-hans/getting-started/install-self-hosted/docker-compose)


