# Docker部署

---

## 1. 本地部署

```bash
docker run -p 5555:5555 -p 5556:5556 -d --name ezwork-ai ehewon/ezwork-ai
#国内加速器
docker run -p 5555:5555 -p 5556:5556 -d --name ezwork-ai dockerpull.com/ehewon/ezwork-ai
```

## 2. 远程部署

### 2.1. 克隆主仓库

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

### 2.2. 更改接口地址

##### 如部署到ip为19.91.9.31的服务器上，映射的端口为5555, 则接口地址为 http://19.91.9.31:5555

* frontend.env 
* admin.env

### 2.3. 重新构建镜像和服务

> `5555` 对应用户端和接口的端口，`5556` 对应管理后台的端口。如果需要更改前端端口，需要更改 `frontend.env` 和 `admin.env` 的接口对应的端口。

```bash
docker build -t ezwork-ai .
docker run -p 5555:5555 -p 5556:5556 -d --name ezwork-ai ezwork-ai
```

### 2.4. 挂载文件存储目录和数据库目录

* 文件存储目录: /app/api/storage, 挂载的本地目录要有读写权限
* 数据库目录: /var/lib/mysql

```bash
docker build -t ezwork-ai .
docker run -p 5555:5555 -p 5556:5556 -v /ezwork/storage:/app/api/storage -v /ezwork/db:/var/lib/mysql -d --name ezwork-ai ezwork-ai
```

## 3. 访问应用

前台访问 http://localhost:5555 来查看前端应用。

后台访问 http://localhost:5556 来查看后台应用。

* 账户：admin@erui.com
* 密码：erui2024

> 如果是远程服务器部署，则localhost更换为服务器IP地址，如 http://19.91.9.31:5555。
