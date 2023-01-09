# 问题描述

在测试类中插入多条数据出现错误，但数据插入成功。  
![在这里插入图片描述](https://img-blog.csdnimg.cn/c3d67f8e6eee42aabf56cfc90472c0e1.png)

# 问题解决

传入给es中saveall语句内的数据可能为空。即，给es的某个数据是空的。  
**因此，可以对空值进行处理**