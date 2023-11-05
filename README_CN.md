# Retro PHP Web Study Environment

> 这是 [Docker NGINX PHP MySQL PhpMyadmin](https://github.com/rzrokon/Docker-NGINX-PHP-MySQL-PhpMyadmin) 的一个分支，做了一些自定义，主要面向 Apple Silicon macOS 用户。

> 这个项目最初是为了我老式的 PHP 和 Web 课程而创建的。因为我使用的是 Apple Silicon Mac，所以我使用了 `arm64v8/phpmyadmin`，如果你使用的是 amd64 架构，可以将它替换为 `phpmyadmin`。

> 如果你需要生产级工具，我建议使用 [DDEV](https://ddev.com/)。（我在修改完这个 repo 后才了解到这个工具）

> 这里的“复古”指的是我的课程，而不是指这个 repo。

##简介

使用 Docker 和 Docker Compose 轻松进行 PHP + MySQL 开发。

通过这个项目，你可以快速搭建以下环境：

- [NGINX](https://hub.docker.com/_/nginx)
- [PHP](https://hub.docker.com/_/php)
- [phpMyAdmin](https://hub.docker.com/r/phpmyadmin/phpmyadmin/)
- [MySQL](https://hub.docker.com/_/mysql/)

内容包括：

- [要求](#要求)
- [配置](#配置)
- [安装](#安装)
- [使用](#使用)

## 要求

确保你的计算机上已安装最新版本的 **Docker** 和 **Docker Compose**。对于 Windows 和 macOS 用户，你需要安装 **Docker Desktop**。如果你是 macOS 用户，推荐使用 [Orbstack](https://orbstack.dev/) 来提升用户体验，替代 Docker Desktop。

克隆这个代码库或将文件复制到一个新文件夹中。在 **docker-compose.yml** 文件中，你可以修改 IP 地址（如果你运行多个容器）或将数据库从 MySQL 更改为 MariaDB。

如果你使用 Linux，确保在使用 Docker 时，将 [将你的用户添加到 `docker` 组](https://docs.docker.com/install/linux/linux-postinstall/#manage-docker-as-a-non-root-user)。

## 配置

编辑 `.env` 文件来修改默认的 IP 地址、MySQL root 密码和数据库名称。

## 安装

打开终端，使用 `cd` 命令切换到包含 `docker-compose.yml` 文件的文件夹，然后运行：

```
docker-compose up
```

这将在 `docker-compose.yml` 文件旁边创建两个新文件夹。

* `data` – 用于存储和还原数据库备份以及初始化数据库以供导入
* `www` – 存放你的 PHP 应用程序文件的位置

容器现在已经构建并正在运行。你应该能够通过浏览器访问 WordPress 安装，使用在配置文件中配置的 IP 地址。默认情况下是 `http://127.0.0.1`。

为了方便起见，你可以将新的主机名添加到你的主机文件中。

## 使用

### 启动容器

你可以使用 `up` 命令以守护进程模式（通过添加 `-d` 参数）启动容器，也可以使用 `start` 命令：

```
docker-compose start
```

### 停止容器

```
docker-compose stop
```

### 删除容器

要停止和删除所有容器，使用 `down` 命令：

```
docker-compose down
```


如果需要删除用于持久化数据库的数据库卷，请使用 `-v` 选项：

```
docker-compose down -v
```

### 从现有源代码创建项目

将 `docker-compose.yml` 文件复制到一个新目录。在该目录中，创建两个文件夹：

* `data` – 在这里添加数据库备份文件或粘贴 `init.sql`
* `web` – 在这里复制你现有的 PHP 项目文件

现在，你可以运行 `up` 命令：

```
docker-compose up
```

这将创建容器并使用提供的备份来填充数据库。

### 创建数据库备份

```
./export.sh
```

### phpMyAdmin

在启动容器后，你可以访问 `http://127.0.0.1:8000` 来访问 phpMyAdmin。

默认用户名是 `root`，密码与 `.env` 文件中提供的密码相同。
