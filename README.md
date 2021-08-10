# Upboard_RT_kernal_compile
## 一、根据自己需求下载相应版本内核和相应的patch文件，本文以4.4.270-rt222为例  
linux内核： https://mirrors.edge.kernel.org/pub/linux/kernel/v4.x/linux-4.4.270.tar.xz  
patch文件： https://mirrors.edge.kernel.org/pub/linux/kernel/projects/rt/4.4/older/patches-4.4.270-rt222.tar.xz  
upboard patch文件：git clone https://github.com/windyfashion/Upboard_RT_kernal_compile.git  

## 二、打patch文件  
解压内核压缩包，将patch压缩包和upboard patch压缩包拷贝到内核文件夹中。  
输入指令：  
`unxz -cd patches-4.4.270-rt222.tar.xz | patch -p1`  
  
`unxz -cd UP-borad-patches.tar.xz | patch -p1`  
注意：需保证patch补丁正确打成。  
  
## 三、编译内核  
1、配置编译选项：  
`make oldconfig`    
注意事项：  
（1）Preemption Model 选择5  
（2）带ACPI的选项要选Y，否则Up board外设无法使用  
（3）Upboard extra选项应选Y  
其他选项按需选择，或者默认选项即可。  
  
2、编译内核  
`fakeroot make -j4 deb-pkg`  
注意事项：  
（1）根据自己电脑配置选择j4或者更高  
（2）需保证电脑硬盘剩余空间有30G以上  
  
3、安装  
编译完毕后，会在上层目录中生成一系列deb文件  
`sudo dpkg -i *.deb`  
  
4、验证  
安装结束以后，更改系统引导文件：  
`sudo gedit /etc/default/grub`  
将GRUB_HIDDEN_TIMEOUT=0注释掉 #GRUB_HIDDEN_TIMEOUT=0  
执行指令 `sudo update-grub` 更新系统引导  
重启系统，在grub页面选择advance......选项，选择刚刚安装的内核（含rt的）  
进入系统，输入`uname -r`，查看是否为刚安装的实时内核，若是则实时内核配置成功。  
输入 `ls /dev/spi*`  
显示 spi2.1和spi2.0，则Up board驱动配置成功  
  
