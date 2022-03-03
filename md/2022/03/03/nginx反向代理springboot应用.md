# nginx反向代理springboot应用.md
0. 安装nginx和启动springboot应用  
1. 配置nginx.conf  
```xml
server
    {
        # 监听端口
        listen 80;
        # 服务名，外部访问地址
        server_name test.com;
        
        location / {
        # 要代理的应用运行的地址和端口号
          proxy_pass http://127.0.0.1:8100;
          index index.html index.htm;
          proxy_set_header Host $host;
          proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        }
        access_log  /test/access.log;
        error_log /test/error.log;
    }
```
2. 重启nginx，访问测试