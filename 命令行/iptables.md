
只开放指定ip

	iptables -A INPUT -s 172.18.104.188 -p all -j ACCEPT
	iptables -A INPUT -s 172.17.164.106 -p all -j ACCEPT
	iptables -A INPUT -j REJECT



	效果
	num  target     prot opt source               destination
	1    ACCEPT     all  --  172.17.164.106       0.0.0.0/0
	2    ACCEPT     all  --  172.18.104.188       0.0.0.0/0
	3    REJECT     all  --  0.0.0.0/0            0.0.0.0/0           reject-with icmp-port-unreachable





只开放指定ip的某个端口

	iptables -I INPUT -p TCP --dport 1521 -j DROP
	iptables -I INPUT -s 172.18.104.188 -p TCP --dport 1521 -j ACCEPT
	iptables -I INPUT -s 172.17.164.106 -p TCP --dport 1521 -j ACCEPT


保存并重启
service iptables save && service iptables restart


查看状态
service iptables status

删除规则
 iptables -D INPUT 1