# VSCode与Android native ELF开发模板项目

## 插件要求
安装CodeLLDB, C/C++, CMake, CMake-tools VSCODE插件，并且需要在系统本地安装

## 预先配置
### 修改NDK CMake Toolchain文件路径
修改.vscode/settings.json中的-DCMAKE_TOOLCHAIN_FILE=ndk cmake toolchain文件路径

### 启动LLDB-Server
在NDK目录下有多种CPU架构的lldb-server，位于toolchains\llvm\prebuilt\windows-x86_64\lib\clang\17\lib\linux目录下，选择aarch64的lldb-server。接下来需要依次执行以下步骤：

#### 1. 在手机上启动lldb-server

把它推送到手机上启动，命令如下，其中platform表示以平台模式运行，--server表示启动一个服务等待连接，--listen表示服务监听在*:2000地址上。
```
./lldb-server platform --server --listen *:2000
```

#### 2. 将手机与电脑通过adb连接, 并转发端口

执行 adb forward tcp:2000 tcp:2000，将手机上的端口转发到电脑本地上