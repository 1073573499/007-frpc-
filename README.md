# 007-frpc-
本人用了大佬移植的007+ipv6远程后发现有一个缺点：移动ipv6无公网，这很遗憾，索性开整frp内网穿透。
准备工具：
007+路由器一台
服务器一台
域名一个（直接用服务器ip也可以）
自己下载或使用仓库里提供的frpc文件
配置好adb后
文件夹内shift+鼠标右键，点击在此处打开命令
然后连接007，输入：adb connect 192.168.0.1:5555
推送frp文件夹里的文件到/home 输入：adb push frp\ /home/
然后进去shell输入：adb shell
Superadmin
he=e47#22u输入超级用户账号和密码
然后挂载给权限，输入：mount -o remount,rw / / ，chmod 777 /home/frp -R

最后添加自启vi /etc/init.d/adbd-init，在exit 0 的上一行里 加入sleep 30 && cd /home/frp && nohup ./frpc -c ./frpc.ini &，然后ESC :wq 回车 保存。
所有操作到此结束，还有点瑕疵是，经测试，部分电脑无法查看最后一步可以采用pull文件修改好后再push上去的方法，教程如下：

adb pull /etc/init.d/adbd-init d:\frp
下载下来后，把cd /home/frp && nohup ./frpc -c ./frpc.ini &h加到exit0之前。
进入shell
adb shell

挂载读写
mount -o remount / /

CTRL+D退出shell

再推回去
adb push d:\frp\adbd-init /etc/init.d


进入shell
adb shell

改权限
chmod 644 /etc/init.d/adbd-init
