java.lang.RuntimeException: java.lang.RuntimeException: org.codehaus.plexus.
## 爆红原因

出现这种报错的原因很可能是[maven](https://so.csdn.net/so/search?q=maven&spm=1001.2101.3001.7020)的版本太高了，我是用的maven版本是3.8.5（2022年发布的），而我的IDEA是2021版本的，所以可能是这个原因报错

## 解决办法

重新下载一个3.6.3的maven版本，并重新配置便可成功。