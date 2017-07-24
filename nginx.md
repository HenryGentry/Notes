# Notes #
### nginx install and config(windows os) ###
1. download nginx in the offical website;
2. unzip;
3. use cmd commands;  


然后你可以在nginx的安装目录下打开windows命令窗口,使用start nginx 启动nginx服务器。再用浏览器打开地址为localhost的网页；  
可以通过命令nginx.exe -s stop停止nginx服务；  
#### nginx config (nginx配置)####
	listen       [端口号];
    server_name  localhost;
    location / {  
		root   [项目路径];  
		index  index.html index.htm;
		try_files $uri /index.html; //配置单页应用时候加上这个
	}

#### nginx config spa(nginx配置单页应用)####
