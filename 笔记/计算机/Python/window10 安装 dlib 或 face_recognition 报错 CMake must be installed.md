
## 安装 dlib 或者 face_recognition

先尝试安装： `pip install dlib` ，如果报错，并且报错信息中有 `CMake` 字样信息：`ERROR: CMake must be installed to build dlib`

1.  说明你需要先下载安装 `Cmake` 这个软件，官网：[https://cmake.org/download/](https://cmake.org/download/)
2. 下载安装后将软件安装目录的 `bin` 文件夹添加到环境变量 `PATH` 中，譬如： `D:\AZ\cmake\bin`

然后重开一个 `cmd` 窗口，并尝试安装 `pip install dlib`，如果遇到 `C++` 的报错信息，需要：

1.  下载安装 `Visual Studio C++`， 官网: [https://visualstudio.microsoft.com/zh-hans/vs/features/cplusplus/](https://visualstudio.microsoft.com/zh-hans/vs/features/cplusplus/)
2.  这里下载的其实是 `Visual Studio Installer`, 打开这个软件，找到 `C++ 的桌面开发` 这个组件，下载安装这个组件后，重启电脑。

再次重新尝试安装 `dlib` 或者 `face_recognition`， 应该就没什么问题了

## 总结
需要下载
`Cmake`软件
VS2019


