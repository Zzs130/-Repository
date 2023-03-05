# docker

## 遇见错误

虚拟化错误
Hardware assisted virtualization and data execution protection must be enabled in the BIOS. See <https://docs.docker.com/desktop/windows/troubleshoot/#virtualization>

![报错](/f9525dcc1c484d10ae8c413878fff567.png)
解决方法
<https://blog.csdn.net/MyronCham/article/details/125216511>

Hyper-V功能已开启但不起作用
管理员身份 命令启动：
> bcdedit /set hypervisorlaunchtype auto
重启电脑，启动docker desktop ，即可

## windows docker 远程

<https://juejin.cn/post/7036698224479993863>
![过程](/Snipaste_2023-01-09_23-52-04.jpg)
双方都要安装docker

192.168.1.108是服务器的 IPv4 地址在ipconfig查看

```ts
netsh interface portproxy add v4tov4 listenport=2375 connectaddress=127.0.0.1 connectport=2375 listenaddress=192.168.1.108 protocol=tcp
```

例子

```ts
docker -H 192.168.1.108:2375 info

docker -H 192.168.1.108:2375 run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=123Qwe123" -p 143:1433 -v /D/gx/data:/var/opt/mssql --name sql2019  -d mcr.microsoft.com/mssql/server:2019-latest

docker exec -it <container_id|container_name> /opt/mssql-tools/bin/sqlcmd -S localhost -U sa -P <your_password>
```

和本地跑docker命令没什么不同

入门
<https://www.jianshu.com/p/c69a2a3b4c7a>

## 安装

<https://zhuanlan.zhihu.com/p/381115119>

### sqlserver

<https://hub.docker.com/_/microsoft-mssql-server>

![运行docker sqlserver](/Snipaste_2023-01-14_17-53-16.jpg)

错误：远程主机强迫关闭了一个现有的连接
解决方法：docker exec -it mssql1 /opt/mssql-tools/bin/sqlcmd -S localhost -U sa -P 123Qwe123

<https://www.cnblogs.com/Fengyinyong/p/13916376.html#:~:text=1.%20%E6%A0%B9%E6%8D%AE%20docker%20inspect%20%3Ccontainer%3E,%E5%91%BD%E4%BB%A4%E6%9F%A5%E7%9C%8Bsqlserver%E5%AE%B9%E5%99%A8%E7%9A%84%E7%BD%91%E7%BB%9C%EF%BC%8C%E5%85%B6%E4%B8%AD%3Ccontainer%3E%20%E4%BB%A3%E8%A1%A8%E8%A6%81%E6%93%8D%E4%BD%9C%E7%9A%84%E5%AE%B9%E5%99%A8%EF%BC%8C%E5%8F%AF%E4%BB%A5%E6%98%AF%E5%AE%B9%E5%99%A8%E7%9A%84name%20%E6%88%96%E8%80%85ID%E3%80%82%202.%E5%AE%B9%E5%99%A8%E5%A4%96%20ssms%E8%BF%9E%E6%8E%A5%E6%95%B0%E6%8D%AE%E5%BA%93%EF%BC%9A%E5%A1%AB%E5%85%A5%E5%AE%B9%E5%99%A8IP%EF%BC%8C%E4%BB%A5%E5%8F%8A%E5%90%AF%E5%8A%A8%E5%AE%B9%E5%99%A8%E6%97%B6%E8%AE%BE%E7%BD%AE%E7%9A%84%E8%B4%A6%E5%8F%B7%E5%AF%86%E7%A0%81%20%E7%99%BB%E5%BD%95%E5%AE%B9%E5%99%A8%E6%95%B0%E6%8D%AE%E5%BA%93%E3%80%82>

多开错误
![多开错误](/Snipaste_2023-01-28_02-28-02.JPG)
docker

### reids

安装
<https://cloud.tencent.com/developer/article/1562815>

### nginx

#### 配置

发布页面

大致操作为以vue为例
docker pull nginx下载镜像，docker images检查是否成功下载
vue项目执行npm run build编译生成dist文件，
执行
docker run --name qihangvue -d -p 3630:80 -v /D/web/dist:/usr/share/nginx/html nginx
该命令作用是生成容器，
其中-v /D/web/dist:/usr/share/nginx/html是将本地D:\web\dist挂载到容器/usr/share/nginx/html
![nginx部署容器](/Snipaste_2023-01-15_22-31-14.JPG)

<https://blog.csdn.net/hnw13938056090/article/details/105782931>

进入容器内
docker exec -it 容器名 bash

更新包管理
apt-get update

安装vim,用来修改Linux中的文件，如deful.conf
apt-get install vim

E492:Not an editor command:qw

先保存再退出即可——：x再：q

#### 反向代理

端口转发
对在容器内、位于etc/nginx/conf.d的default.conf文件添加以下内容

```TS
location /api/qihangapi {
   proxy_pass http://192.168.1.108:8133/qihangapi;
   }
```

可以简单理解为<http://localhost:80/api/qihangapi>转发到<http://192.168.1.108:8133/qihangapi>

<https://www.cnblogs.com/yucongblog/p/13428535.html>

## .net core

配置Dockerfile,.dockernignore文件
qihang-api整个源码项目放到装有docker服务器中，在根目录中执行
docker build -f QiHangApi.Web/Dockerfile -t qihangapi .
<https://www.cnblogs.com/xhznl/p/13353095.html>

## 更改docker安装到非C盘（Windows）

mklink使用

更改win子系统
wsl迁移

```ts
wsl -l -v
```

<https://blog.csdn.net/sg_knight/article/details/118608384#:~:text=%E9%85%8D%E7%BD%AE%20Win10%E5%AD%90%E7%B3%BB%E7%BB%9F%20%E5%B9%B6%20%E4%BF%AE%E6%94%B9%E5%AE%89%E8%A3%85%20%E4%BD%8D%E7%BD%AE%20gold0523%E7%9A%84%E4%B8%93%E6%A0%8F%205010%201.,%E5%8A%9F%E8%83%BD%E2%80%9D%203.%20%E5%8B%BE%E9%80%89%E2%80%9C%E9%80%82%E7%94%A8%E4%BA%8E%20Linux%20%E7%9A%84%20Windows%E5%AD%90%E7%B3%BB%E7%BB%9F%20%E2%80%9D%EF%BC%8C%E5%B9%B6%E5%8D%95%E5%87%BB%E7%A1%AE%E5%AE%9A%E3%80%82%204.>
