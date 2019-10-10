# 搭建nginx图片服务器windows版

1. 下载windows版的nginx，解压

2. 修改nginx.conf配置,增加一个server节点 

   ```nginx
   server {
           listen       8123;
           server_name  localhost;
   
           charset utf-8; 
   
           #access_log  logs/host.access.log  main;
   
   		location ~ .*\.(gif|jpg|jpeg|png)$ {          
   		expires 24h;              
   		root C:/Users/Administrator/Desktop/html/;#指定图片存放路径              
   		access_log C:/Users/Administrator/Desktop/html/img_nginx.log;#图片路径              
   		proxy_store on;              
   		proxy_store_access user:rw group:rw all:rw;              
   		proxy_temp_path C:/Users/Administrator/Desktop/html/;#图片路径             
   		proxy_redirect          off;                
   		proxy_set_header        Host 127.0.0.1;              
   		proxy_set_header        X-Real-IP $remote_addr;              
   		proxy_set_header        X-Forwarded-For $proxy_add_x_forwarded_for;             
   		client_max_body_size    10m;              
   		client_body_buffer_size 1280k;              
   		proxy_connect_timeout   900;              
   		proxy_send_timeout      900;              
   		proxy_read_timeout      900;              
   		proxy_buffer_size       40k;              
   		proxy_buffers           40 320k;              
   		proxy_busy_buffers_size 640k;              
   		proxy_temp_file_write_size 640k;
           #这里如果没有找到图片 就返回404 not found ，亲测可以
   		if ( !-e $request_filename) {                   
   			#proxy_pass  http://127.0.0.1:8089;   #代理访问地址
   			return 404;
   			}      
   		} 
   ```

   3. 访问

      <http://localhost:8123/fl.png>



## windows下启动，停止等nginx命令

首先进到解压好的nginx文件夹中

#### 启动

start nginx.exe

#### 停止

nginx.exe -s stop

#### 重启

nginx.exe -s reload