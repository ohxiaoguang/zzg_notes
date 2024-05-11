一、rich-rule实现IP端口限制访问
1、添加规则
firewall-cmd --permanent --add-rich-rule="rule family="ipv4" source address="10.51.54.1" port protocol="tcp" port="9201" accept"

批量添加网段
firewall-cmd --permanent --add-rich-rule="rule family="ipv4" source address="10.51.54.1/24" port protocol="tcp" port="9201" accept"

暴露端口
#开启某个端口（所有IP可访问）
firewall-cmd --permanent --zone=public --add-port=80/tcp
#删除策略：
firewall-cmd --permanent --zone=public --remove-port=80/tcp

2、生效规则
firewall-cmd  --reload

3、查看结果
firewall-cmd --list-all

4、批量添加屏蔽ip网段
firewall-cmd --permanent --zone="public" --add-rich-rule="rule family="ipv4" source address="10.30.125.0/24" drop"

二、firewall-cmd常用命令
查看防火墙状态
firewall-cmd --state

查看防火墙
firewall-cmd --list-all

更新防火墙规则
firewall-cmd  --reload

服务
防火墙服务的状态
systemctl status firewalld.service

启动/关闭 防火墙
systemctl start firewalld.service
systemctl stop firewalld.service