# redis安装 Linux版

1. 下载redis-5.0.4.tar.gz压缩包，并上传至centos上

2. 解压文件

   ```shell
   tar -xvf redis-5.0.4.tar.gz
   ```

3. redis需要对源码进行编译才能使用

   ![1570800278724](.\redis安装Linux版.assets\1570800278724.png)

4. 注意，redis.conf不在src目录中，而在它的上一级../

   ![1570800388681](.\redis安装Linux版.assets\1570800388681.png)

5. 连接redis客户端

   ```shell
   1. cd redis-5.0.4
   2. cd src
   3. ./redis-cli
   ```

6. 修改redis.conf,允许远程，同时要记得开放端口

   ![1570800581874](.\redis安装Linux版.assets\1570800581874.png)

   

   ![1570800742487](.\redis安装Linux版.assets\1570800742487.png)

7. 使用RDM（redis desktop manager）客户端连接redis服务

   