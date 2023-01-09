## 一、sys.path.append（）

1、明确自己下载的库/包安装路径，我的默认下载到了E:\Anaconda\Lib\site-packages

2、在Spyder窗口或者Anaconda Prompt输入：

import sys
sys.path.append('库/包的路径')


此方法每次启动都要重新做一遍。

## 二、添加搜索路径 永久解决问题

1、明确自己下载的库/包安装路径，我的默认下载到了E:\Anaconda\Lib\site-packages

2、找到运行环境的site-packages文件，在里面创建txt文档，txt里面输入库/包的路径，保存，重命名为.pth文件。

比如我的：在E:\Anaconda\envs\spyder-cf\Lib\site-packages下创建txt文档，txt内输入E:\Anaconda\Lib\site-packages，保存，重命名为mypkpath.pth。
————————————————
版权声明：本文为CSDN博主「秦天一」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/ShaoShuaiQ/article/details/126600444