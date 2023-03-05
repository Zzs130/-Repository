# ubuntu  and proxmox

## pve

### 修改PVE虚拟机硬件参数

在pve shell命令行关闭虚拟机

```ts
//查看虚拟机id
qm list
//关闭id为100的虚拟机
qm stop 100

```

重启即可更新硬件参数

### pve省电模式

<https://pve.sqlsec.com/4/6/>

### 创建CT

<https://blog.csdn.net/hanzheng260561728/article/details/125688892>

### nano文本编辑器

^C --- ctrl+c
^O --- 同理ctrl+o

<https://cloud.tencent.com/developer/article/1935086>

## ubuntu

更新

```ts
sudo apt-get update
```

### ssh远程连接

```Ts
//查看是否安装ssh及状态
sudo service ssh stuts
```

### samba共享

<https://zhuanlan.zhihu.com/p/412742041>

#### 文件夹权限

<https://zhuanlan.zhihu.com/p/255000117>

#### vi对文件修改

<https://www.runoob.com/linux/linux-vim.html>