# MacOS部署

---

## 概述

本文档详细描述了如何在全新的 macOS 系统上从头开始部署 EzWork 项目。EzWork 项目由 Python 后端、PHP 前端和 MySQL 数据库组成。以下将详细说明每个组件的安装与配置。

## 环境要求

- macOS 操作系统
- 必要的工具：`git`, `curl`, `brew`
- 运行以下命令前，请确保您具有管理员权限。

## 步骤概述

1. 更新系统和安装必要的工具
2. 安装 Python 和相关包
3. 安装 PHP 和必要的扩展
4. 安装 MySQL 数据库
5. 下载并配置 EzWork 项目
6. 启动服务并配置数据库

## 1. 更新系统和安装必要的工具

首先，确保您的 macOS 系统是最新的。然后，安装 Homebrew（如果还没有安装的话），这是一个用于安装软件包的工具：

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

更新 Homebrew 并安装常用工具：

```bash
brew update
brew install git curl wget node
```

## 2. 安装 Python 和相关包

接下来，安装 Python 3.9（根据项目需要安装的版本）及所需的 Python 库。

### 安装 Python 3.9

使用 Homebrew 安装 Python 3.9：

```bash
brew install python@3.9
```

确保 Python 和 pip 已成功安装：

```bash
python3.9 --version
pip3 --version
```

### 安装所需的 Python 包

```bash
# 安装所需的 Python 包
pip3 install openpyxl lxml openai pydantic_core python-docx==1.1.2 python-pptx pdf2docx pymysql PyMuPDF==1.24.7 docx2pdf python-dotenv pytesseract
```

## 3. 安装 PHP 和必要的扩展

### 安装 PHP 8.2

使用 Homebrew 安装 PHP 8.2：

```bash
brew install php@8.2
```

### 启动 PHP 服务

在 macOS 上启动 PHP 服务：

```bash
brew services start php@8.2
```

## 4. 安装 MySQL 数据库

### 安装 MySQL

使用 Homebrew 安装 MySQL：

```bash
brew install mysql
```

### 启动 MySQL 服务

```bash
brew services start mysql
```

### 配置 MySQL

设置 MySQL root 用户密码并创建数据库：

```bash
mysql_secure_installation

# 登录 MySQL
mysql -uroot -p

# 创建数据库和用户并授权
CREATE DATABASE ezwork;
```

### 初始化数据库

在您项目的 `init.sql` 文件中创建所需的表和初始数据。例如：

将上述 SQL 语句运行到 MySQL 中。

```bash
mysql -uroot -p ezwork < ./init.sql
```

## 5. 下载并配置 EzWork 项目

### 克隆项目代码

```bash
cd /var/www
git clone https://github.com/EHEWON/ezwork-ai-doc-translation.git ezwork
cd ezwork
git checkout master
git submodule update --init --recursive
cd api
git checkout master
git pull
curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
composer install
cd ../frontend
git checkout master
git pull
cd ../admin
git checkout master
git pull
cd ..
```

### 配置 `.env` 文件

在 `api` 目录下创建 `.env` 文件并添加数据库连接信息：

```env
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=ezwork
DB_USERNAME=ezworkuser
DB_PASSWORD=your_password

#设置邮件系统
MAIL_DRIVER=smtp
MAIL_HOST=s
MAIL_PORT=80
MAIL_USERNAME=
MAIL_PASSWORD=
MAIL_FROM_ADDRESS=
MAIL_FROM_NAME='Ehe Admin'
```

## 6. 启动服务

### 启动 PHP 服务

确认 PHP 正在运行：

```bash
brew services list
```

### 启动 Nginx

如果您需要通过 Nginx 作为反向代理来处理 HTTP 请求，可以使用 Homebrew 安装并配置 Nginx：

```bash
brew install nginx
```

### 配置 Nginx

在 `/usr/local/etc/nginx/servers/` 目录下创建一个新的配置文件（如 `ezwork`），并添加以下内容：

```nginx
server {
    listen 80;
    server_name your_defiend_doamin;  #定义访问域名

    root /var/www/ezwork/api/public;
    index index.php;

    location /api/ {
        try_files $uri $uri/ /index.php?s=$1; 
    }

    location /storage/ {
        alias /var/www/ezwork/api/storage/app/public/;
        try_files $uri $uri/ =404;
    }

    location ~ \.php$ {
        root /var/www/ezwork/api/public;
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php8.2-fpm.sock;
        #fastcgi_pass 127.0.0.1:9000; #另一种替代写法
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        include fastcgi_params;
    }
}
```

### 更改本地hosts

```bash
vi /etc/hosts
#末尾添加一条：
127.0.0.1 your_defiend_doamin
```

### 启动 Nginx

```bash
brew services start nginx
```

修改frontend.env文件中的api接口地址。 修改完后拷贝到frontend目录
```bash
cp frontend.env frontend/.env
```

修改admin.env文件中的api接口地址。 修改完后拷贝到admin目录
```bash
cp admin.env admin/.env
```

### 运行用户端

```bash
cd /var/www/ezwork/frontend
sudo yarn 
sudo yarn dev
```

### 运行管理后台端

```bash
cd /var/www/ezwork/admin
sudo yarn
sudo yarn dev
```