
可能是pip版本的问题，但是不知道哪个版本是对的，不找了，直接<font color="#ff0000">源文件安装</font>吧

[https://pypi.tuna.tsinghua.edu.cn/simple/opencv-python/](https://pypi.tuna.tsinghua.edu.cn/simple/opencv-python/)

放到本地目录[D:\Anaconda\Lib\site-packages]，
直接pip install opencv_python-4.1.1-cp37-cp37m-win_amd64.whl安装成功


其余方法
## No module named ’ 安装包名字’ 
百度查解决方法，方法有很多，比如

方法一：pip install 安装包名字

方法二：python -m pip install 安装包名字

方法三：pip --trusted-host pypi.python.org install 安装包名字

## Could not find a version that satisfies the requirement 安装包名字 
查问题会提示换成国内的pip源 可以解决问题

方法一：pip install 安装包名字 -i http://pypi.doubanio.com/simple/ --trusted-host pypi.doubanio.com //豆瓣镜像网站

方法二：pip install 安装包名字 -i http://pypi.douban.com/simple/ --trusted-host pypi.douban.com //豆瓣

方法三：pip install 安装包名字 -i https://pypi.tuna.tsinghua.edu.cn/simple/ --trusted-host pypi.tuna.tsinghua.edu.cn //清华大学
