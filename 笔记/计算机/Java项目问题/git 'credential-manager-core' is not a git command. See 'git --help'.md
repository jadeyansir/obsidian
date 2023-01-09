git pull  
git: 'credential-manager-core' is not a git command. See 'git --help'.

![](https://img2020.cnblogs.com/blog/1499639/202107/1499639-20210707152442800-1472119689.png)

看了好多教程，最后找到了这篇！！！！[https://ask.csdn.net/questions/5465673](https://ask.csdn.net/questions/5465673)  
（更新：今天看这个链接竟然已经失效了emmm，感谢不知名朋友的一个推荐！）

**This sounds as if GCM Core was not installed correctly into your Git's libexec path. What does git --exec-path show? Do you see git-credential-manager-core.exe in that folder? If not, can you find where it was installed instead?**

就是说，git --exec-path，打开所示目录  
![](https://img2020.cnblogs.com/blog/1499639/202107/1499639-20210707152808649-1594956201.png)  
然后发现目录下没有git-credential-manager-core.exe  
然后去下载git-credential-manager-core.exe【但是用everything检索会发现我是有这个的，只是不在这个目录下，下载完还是不在这个目录下，但是git pull就没问题了。。。】  
[https://github.com/microsoft/Git-Credential-Manager-Core/releases/tag/v2.0.475](https://github.com/microsoft/Git-Credential-Manager-Core/releases/tag/v2.0.475)  
![](https://img2020.cnblogs.com/blog/1499639/202107/1499639-20210707152508020-50435567.png)

安装exe，成功！！！！  
![](https://img2020.cnblogs.com/blog/1499639/202107/1499639-20210707152704506-247163504.png)

也是因为这个，所以每次git pull都要输入用户名密码！！不知道为什么有一天突然就这样了！！！