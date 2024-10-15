# EZ-work文档翻译

人人可用的AI文档翻译助手，可以快速低成本调用OpenAI等大语言模型api，帮助您实现txt、word、csv、excel、pdf、ppt的文档翻译。

- 支持txt、word、csv、excel、pdf、ppt文档AI翻译
- 支持扫描pdf翻译
- 支持兼容OpenAI格式的任何端点API（中转API）
- 支持批量操作
- 支持多线程
- 支持Docker部署

## 程序截图

### 用户前台

![图片](https://github.com/user-attachments/assets/d2fcf98a-4c6e-4c4a-a2ae-8d5d5cc81173)


### 管理后台

![图片](https://github.com/user-attachments/assets/d4781a49-917b-4a1e-a0fc-6673825bd2ff)

## 使用方法

本程序兼容OpenAI API请求格式进行文档翻译，请输入接口地址，默认为https://api.openai.com （支持中转接口），再输入API Key，即可开始使用。

在线版无需注册即可体验，暂不提供会员注册服务。如果您需要完整的功能和更快的性能，请按照下方提示自行部署。

## 翻译效果

### 原文

![图片](https://github.com/user-attachments/assets/55959e59-3e28-4aa9-91d4-a936f1bb1fa7)


### 译文

![图片](https://github.com/user-attachments/assets/b06eb00e-7b9d-434b-ae8b-43b84afcbbac)


## 项目安装与配置文档

### 目录

- [前言](#前言)
- [环境要求](#环境要求)
- [克隆主仓库](#克隆主仓库)
- [更新子模块](#更新子模块)
- [修改 .env 文件](#修改-env-文件)
- [Docker Compose 配置](#docker-compose-配置)
- [构建与启动服务](#构建与启动服务)
- [访问应用](#访问应用)
- [常见问题](#常见问题)

### 前言

本项目由四个主要部分组成：`api`、`frontend`、`admin` 和主仓库。主仓库使用 Git 子模块的方式引用其他三个仓库。我们将使用 Docker Compose 来部署这些服务。

### 环境要求

在开始之前，请确保你的系统上安装了以下软件：

- [Docker](https://docs.docker.com/get-docker/) - 用于容器化应用。
- [Docker Compose](https://docs.docker.com/compose/install/) - 用于定义和运行多容器 Docker 应用。
- [Git](https://git-scm.com/) - 用于版本控制和代码管理。


# 使用 Docker 启动 ezwork-ai 服务

## 1. 直接启动服务

```bash
docker pull ehewon/ezwork-ai
docker run -p 5555:80 -p 5556:8080 -d --name ezwork-ai ehewon/ezwork-ai
```

## 2. 针对有修改需求的，重新构建服务

### 克隆主仓库

首先，克隆主仓库到本地，并更新子模块：

```bash
git clone https://github.com/EHEWON/ezwork-ai-doc-translation.git ezwork-ai-doc-translation
cd ezwork-ai-doc-translation
git checkout master
git submodule update --init --recursive
cd api
git checkout master
git pull
cd ../frontend
git checkout master
git pull
cd ../admin
git checkout master
git pull
cd ..
```

### 重新构建镜像和服务

> `5555` 对应用户端和接口的端口，`5556` 对应管理后台的端口。如果需要更改前端端口，需要更改 `frontend.env` 和 `admin.env` 的接口对应的端口。

```bash
docker build -t ezwork-ai .
docker run -p 5555:80 -p 5556:8080 -d --name ezwork-ai ezwork-ai
```


### 访问应用

Frontend: 访问 http://localhost:5555 来查看前端应用。

Backend: 访问 http://localhost:5556 来查看后台应用。
* 账户：admin@erui.com
* 密码：erui2024


### 常见问题
1. 如何停止服务？
要停止所有服务，可以运行：
```bash
docker stop ezwork-ai
```

#### 2. 如何查看日志？
要查看服务的日志，可以使用：
```bash
docker logs ezwork-ai
```

### 4. 如何访问数据库？
你可以通过 MySQL 客户端连接到数据库，使用以下连接信息：
```bash
docker exec -it ezwork-ai mysql -uroot -pezwork ezwork
```

## 其他系统的部署教程

- [CentOS 系统](https://github.com/EHEWON/ezwork-ai-doc-translation/blob/main/build/Centos.md) - 请查看此文件获取在 CentOS 系统上的部署步骤。
- [Ubuntu 系统](https://github.com/EHEWON/ezwork-ai-doc-translation/blob/main/build/Ubuntu.md) - 请查看此文件获取在 Ubuntu 系统上的部署步骤。
- [Macos 系统](https://github.com/EHEWON/ezwork-ai-doc-translation/blob/main/build/Macos.md) - 请查看此文件获取在 Macos 系统上的部署步骤。

## 微信交流群

![图片](https://github.com/user-attachments/assets/f35d7bed-2e5a-4b36-b954-0d83c93ac660)


## Star History

[![Star History Chart](https://api.star-history.com/svg?repos=EHEWON/ezwork-ai-doc-translation&type=Date)](https://star-history.com/#/EHEWON/ezwork-ai-doc-translation&Date)
