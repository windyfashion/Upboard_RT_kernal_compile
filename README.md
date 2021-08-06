# Upboard_RT_kernal_compile
## 一、根据自己需求下载相应版本内核和相应的patch文件，本文以4.4.270-rt222为例
linux内核： https://mirrors.edge.kernel.org/pub/linux/kernel/v4.x/linux-4.4.270.tar.xz
patch文件： https://mirrors.edge.kernel.org/pub/linux/kernel/projects/rt/4.4/older/patches-4.4.270-rt222.tar.xz
upboard patch文件：

## 二、打patch文件
解压内核压缩包，将patch压缩包和upboard patch压缩包拷贝到内核文件夹中。
输入指令：
unxz -cd patches-4.4.270-rt222.tar.xz | patch -p1
unxz -cd UP-borad-patches.tar.xz | patch -p1

## 三、编译内核
配置编译选项：make oldconfig
注意编译时：
