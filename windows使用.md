# Windows

## 共享文件夹/远程桌面

guest账户启用
此电脑右键管理>本地用户和组中>Guest接除禁用

server 服务未开启，导致右键文件夹无共享

网络密码错误

用户：主机名\用户
例子：
win8\Administrator
123123
微软账号远程登录
microsoft account\xxx.@qq.com
（账号密码）

## 远程sqlserver

开启SQLServerBrowser服务
SQLServer配置管理器>SQL Server网络配置>MSSQLSERVER的协议>TCP/IP启用
防火墙入站

## Office

### 激活

F:\work\Office Tool 运行office tool pluse.exe
激活选项》填入kms主机：kms.luochenzhimu.com 点击激活
 <https://www.bilibili.com/read/cv8944052/>

## mklink使用

<https://www.icoa.cn/a/910.html>

mklink /j "C:\Program Files\Docker" "D:\Program Files\Docker"
拒绝访问，权限问题，PowerShell中进入cmd
![mklink](\Snipaste_2023-01-06_18-57-21.JPG)
