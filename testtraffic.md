tc网络连接故障
```
  该命令将 eth0 网卡的传输设置为随机丢掉 1% 的数据包。
  tc  qdisc  add  dev  eth0  root  netem  loss  1%
  tc  qdisc  add  dev  docker0  root  netem  loss  1%
  该命令将 eth0 网卡的传输设置为延迟 100ms ± 10ms （90 ~ 110 ms 之间的任意值）发送。
  tc  qdisc  add  dev  eth0  root  netem  delay  100ms  10ms
  tc  qdisc  add  dev  docker0  root  netem  delay  100ms  10ms
  恢复网卡故障
  tc qdisc del dev eth0 root
  tc qdisc del dev docker0 root
  ```
iptables网络连接拒绝
  ```
  iptables 故障
  iptables -I INPUT -s 10.125.38.27 -j DROP

  查看是否生效
  iptables -L

  恢复ipptables故障
  iptables -D INPUT -s 10.125.38.27 -j DROP
  ```
ddos攻击
  ```
  hping3安装：https://www.cnblogs.com/emrysche/articles/9352034.html
  使用
    https://blog.csdn.net/huangbaokang/article/details/83901377
    https://blog.csdn.net/u010390063/article/details/79078793
  ```
dd磁盘占满
   ```
   创建
   dd if=/dev/zero of=./bill_test bs=1G count=10
   删除
   rm bill_test
   ```
关机
  ```
  reboot
  ```
