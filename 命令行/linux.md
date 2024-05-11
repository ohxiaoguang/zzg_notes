linux
Ubuntu18.04安装时修改镜像地址 http://mirrors.aliyun.com/ubuntu     或  安装后修改  /etc/apt/sources.list

允许root登录:
```
sudo passwd root
su root
修改             /etc/ssh/sshd_config    PermitRootLogin yes
重启ssh        /etc/init.d/ssh restart
```


配置 IP
编辑 `vi /etc/netplan/50-cloud-init.yaml` 配置文件，修改内容如下
```
network:
    ethernets:
        ens33:
          addresses: [192.168.141.110/24]
          gateway4: 192.168.141.2
          nameservers:
            addresses: [192.168.141.2]
    version: 2
```
使用 netplan apply 命令让配置生效

配置主机名
```
# 修改主机名
hostnamectl set-hostname kubernetes-master
# 配置 hosts
cat >> /etc/hosts << EOF
192.168.141.110 kubernetes-master
EOF
```