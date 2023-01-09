SwitchHosts下载

问题
Win10系统 使用SwitchHosts时，提示没有写入Hosts文件权限

解决方案
1、打开如下目录
C:\Windows\System32\drivers\etc

2、右键 hosts 文件 -> 点击属性 -> 去掉 属性的只读 勾选框
 上述操作完成后以管理员身份运行（管理员都是完全控制的），如果还不行请按如下配置

3、点击安全 -> 点击编辑 -> 找到Users 和自己的用户名，勾选完全控制。

4、配置成功