# Linux的基础知识

### 虚拟机的克隆与快照

* 克隆：即从一个已经存在的系统上，复制一个新的一模一样的实例

  1. 

     ![1570027895948](.\3Linux的基础知识.assets\1570027895948.png)

     ![1570028297255](.\3Linux的基础知识.assets\1570028297255.png)
     
     2. 虚拟机中的当前状态，下一步
     
     ![1570028598977](.\3Linux的基础知识.assets\1570028598977.png)
     
     3. 创建完整克隆
     
        ![1570028677492](.\3Linux的基础知识.assets\1570028677492.png)
     
        4. 选择实例名称，和克隆的位置
     
           ![1570028843303](.\3Linux的基础知识.assets\1570028843303.png)
           
           ![1570029115549](.\3Linux的基础知识.assets\1570029115549.png)
     
     

* 快照：即从一个已经存在的虚拟机系统上，创建一个还原点，当操作系统出现各种错误时，还原到快照时的状态

  1. 拍摄快照

     ![1570029213024](.\3Linux的基础知识.assets\1570029213024.png)

     2. 快照描述

        ![1570029322465](.\3Linux的基础知识.assets\1570029322465.png)

     3. 管理快照，可以做删除等操作

        ![1570029399392](.\3Linux的基础知识.assets\1570029399392.png)

        ​	![1570029426460](.\3Linux的基础知识.assets\1570029426460.png)

        4. 恢复快照

           ![1570029557238](.\3Linux的基础知识.assets\1570029557238.png)

        

        ### Linux的目录结构

        | 目录 | 用途                             | 重要性 |
   | ---- | -------------------------------- | ------ |
        | bin  | 存放二进制文件                   | 高     |
        | dev  | 存放硬件文件                     | 高     |
        | etc  | 存放程序的配置文件               | 高     |
        | home | 非root用户的目录文件             | 普通   |
        | proc | 存放正在运行中的进程文件         | 高     |
        | root | root用户目录                     | 高     |
        | sbin | 存放root用户可以执行的二进制文件 | 高     |
        | tmp  | 存放系统临时文件                 | 低     |
        | usr  | 存放安装的程序                   | 高     |
        | var  | 存放程序或者系统日志文件         | 高     |
        
        ### 常用的基本命令
        
        - 创建文件命令
        
        ```shell
          touch demo.txt
        ```
        
        - 编辑文件命令
        
        ```shell
          vi demo.txt
          编辑：i
          退出编辑： 按esc键
          保存退出： :wq
        ```
        
        - 创建文件夹命令
        
        ```shell
          mkdir school
        ```
        
        - 删除文件或者文件夹命令，-rf：递归并强制不询问删除。
        
        ```shell
          rm -rf demo.txt
          rm -rf shcool
        ```
        
        - 查看运行中的进程列表
        
        ```shell
          ps aux
        ```
        
        - 关闭进程
        
        ```shell
          kill -9 进程编号
        ```
        
        - 关闭SELinux（Linux系统上捆绑的一个安全模块，安装时会和很多软件起冲突，建议关闭）
        
          - 编辑文件
        
          ```shell
          vi /etc/selinux/config
          ```
        
          - 设置 SELINUX=disabled，重启系统（reboot）
        
        
        
        
        
        ### yum
        
        > Yum 全称为 Yellow dog Updater Modified，它是一个在线的软件安装命令。
        >  能够从指定的服务器自动下载RPM包并且安装，可以自动处理依赖性关系，并且一次安装所有依赖的软体包，无须繁琐地一次次下载、安装。yum提供了查找、安装、删除某一个、一组甚至全部软件包的命令，而且命令简洁而又好记。
        
        1. 替换网易yum源 ---->
        
           ```shell
            curl -o /etc/yum.repos.d/CentOS-Base.repo mirrors.163.com/.help/CentOS7-Base-163.repo
           ```
        
        2. 更新缓存
        
           ```shell
            yum clean all 
            yum makecache
           ```
        
           执行1,2即可使用网易的yum源了。
        
        ![1570031697484](.\3Linux的基础知识.assets\1570031697484.png)
        
        
        
        ### 安装mysql
        
        #### 在线安装
        
        1. 下载rpm文件
        
        ```shell
          yum localinstall https://repo.mysql.com//mysql80-community-release-el7-1.noarch.rpm
        ```
        
        2. 安装MySQL数据库
        
        ```shell
          yum install mysql-community-server -y
        ```
        
        #### 本地安装
        
        - 把本课程git工程里共享的MySQL本地安装文件上传到Linux主机的/root/mysql目录
        - 执行解压缩
        
        ```shell
          tar xvf mysql-8.0.11-1.el7.x86_64.rpm-bundle.tar
        ```
        
        - 安装依赖的程序包
        
        ```shell
          yum install perl -y
          yum install net-tools -y
        ```
        
        - 卸载mariadb程序包
        
        ```shell
          rpm -qa|grep mariadb 查出要卸载的mariadb
          rpm -e mariadb-libs-5.5.60-1.el7_5.x86_64 --nodeps
        ```
        
        - 安装MySQL程序包
        
        ```shell
          rpm -ivh mysql-community-common-8.0.11-1.el7.x86_64.rpm 
          rpm -ivh mysql-community-libs-8.0.11-1.el7.x86_64.rpm 
          rpm -ivh mysql-community-client-8.0.11-1.el7.x86_64.rpm 
          rpm -ivh mysql-community-server-8.0.11-1.el7.x86_64.rpm 
        ```
        
        - 修改MySQL目录权限
        
        ```shell
          chmod -R 777 /var/lib/mysql/
        ```
        
        - 初始化MySQL
        
        ```shell
          mysqld --initialize
          chmod -R 777 /var/lib/mysql/*
        ```
        
        - 启动MySQL
        
        ```shell
          service mysqld start
        ```
        
        - 查看初始密码
        
        ```shell
          grep 'temporary password' /var/log/mysqld.log
        ```
        
        - 登陆数据库之后，修改默认密码
        
        ```mysql
          mysql -u root -p [查看到的密码]
          alter user user() identified by "abc123456"; 
        ```
        
        - 允许远程使用root帐户
        
        ```mysql
          use mysql
          UPDATE user SET host = '%' WHERE user ='root';
          FLUSH PRIVILEGES;
        ```
        
        - 允许远程访问MySQL数据库（/etc/my.cnf）
        
        ```ini
          character_set_server = utf8
          bind-address = 0.0.0.0
        ```
        
        ![1570109498950](.\3Linux的基础知识.assets\1570109498950.png)
        
        
        
        * 重新启动mysql
        
          ```shell
          service mysqld restart
          ```
        
        
        
        - 开启防火墙3360端口
        
        ```shell
          firewall-cmd --zone=public --add-port=3306/tcp --permanent
          firewall-cmd --reload
        ```
        
        
        
        