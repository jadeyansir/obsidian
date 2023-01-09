出现这个错误是通用Mapper初始化的错误，排查的方向就是往这个方向，可能的情况有以下几种：

1.jar包冲突
```xml
<dependency>
<groupId>tk.mybatis</groupId>
<artifactId>mapper</artifactId>
<version>3.3.9</version>
</dependency>
<dependency>
   <groupId>tk.mybatis</groupId>
   <artifactId>mapper-spring-boot-starter</artifactId>
   <version>2.0.0</version>
</dependency>
```
如图所示这里有两个tk.mybatis通用Mapper的包了，所以springboot不知道该初始化哪个

<dependency>
   <groupId>tk.mybatis</groupId>
   <artifactId>mapper-spring-boot-starter</artifactId>
   <version>2.0.0</version>
</dependency>
这里使用这个包，重启后运行正常