## VMware

> VMWare (Virtual Machine ware)是一个“[虚拟PC](http://www.baidu.com/s?wd=虚拟PC&tn=SE_PcZhidaonwhc_ngpagmjz&rsv_dl=gh_pc_zhidao)”软件公司.它的产品可以使你在一台机器上同时运行二个或更多Windows、DOS、[LINUX系统](http://www.baidu.com/s?wd=LINUX系统&tn=SE_PcZhidaonwhc_ngpagmjz&rsv_dl=gh_pc_zhidao)。

## Linux

> Linux（i/ˈlɪnəks/ LIN-əks）是一种自由和开放源码的类UNIX [操作系统](http://www.baidu.com/s?wd=操作系统&tn=SE_PcZhidaonwhc_ngpagmjz&rsv_dl=gh_pc_zhidao)。
>
> ​	redhat是基于linux内核的发行版系统，本身并不收费，但升级及其他服务要收费；	
>
> 		* centOS是redhat社区版服务器系统
> 		* fedora是redhat的新技术试验田

## centOS7安装

地址：[https://mirrors.aliyun.com/centos/7/isos/x86_64/CentOS-7-x86_64-Everything-1908.iso](https://mirrors.aliyun.com/centos/7/isos/x86_64/CentOS-7-x86_64-Everything-1908.iso)

安装步骤：

1. 新建虚拟机，选择典型，下一步

   ![1570012837830](.\1VMware安装.assets\1570012837830.png)

2. 稍后安装操作系统，下一步

   ![1570012922252](.\1VMware安装.assets\1570012922252.png)

3. 选择客户机操作系统

   

   ![1570012993541](.\1VMware安装.assets\1570012993541.png)

4. 命名虚拟机

   ![1570013114794](.\1VMware安装.assets\1570013114794.png)

5. 指定磁盘容量

   ![1570013156861](.\1VMware安装.assets\1570013156861.png)

6. 自定义硬件

   ![1570013181924](.\1VMware安装.assets\1570013181924.png)

7. 处理器--->选择虚拟化引擎第一个，因为后期用到的docker需要它

   ![1570013259024](.\1VMware安装.assets\1570013259024.png)

   8. 选择iso映像文件

      ![1570013496861](.\1VMware安装.assets\1570013496861.png)

   9. 不选用共享主机的ip，而选择桥接模式，直接连接到物理网路，拥有自己的ip地址

      ![1570013588381](.\1VMware安装.assets\1570013588381.png)

   10. 点击完成

       ![1570013658929](.\1VMware安装.assets\1570013658929.png)

   11. 开启虚拟机安装centos

       ![1570013753685](.\1VMware安装.assets\1570013753685.png)

   12. 上下键选择install centos 7，回车

       ![1570013828938](.\1VMware安装.assets\1570013828938.png)

   13. 选择语言

       ![1570013973039](.\1VMware安装.assets\1570013973039.png)

   14. 选择安装位置

       ![1570014028205](.\1VMware安装.assets\1570014028205.png)

       点击完成，自动分区

       ![1570014057476](.\1VMware安装.assets\1570014057476.png)

   15. 打开网络

       ![1570014140319](.\1VMware安装.assets\1570014140319.png)

   16. 点击开始安装

       ![1570014192296](.\1VMware安装.assets\1570014192296.png)

   17. 设置超级用户root密码

       ![1570014232361](.\1VMware安装.assets\1570014232361.png)![1570014269634](.\1VMware安装.assets\1570014269634.png)

   18. 安装完成

       ![1570014754758](.\1VMware安装.assets\1570014754758.png)

   

   

   



