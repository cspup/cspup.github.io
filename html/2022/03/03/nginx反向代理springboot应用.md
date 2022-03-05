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
3. 如果配置的proy_pass地址和nginx不在同一机器上则需要开启防火墙保证代理地址可被nginx访问到。例如：代理地址为1.1.1.1:8080,而nginx所在机器地址为2.2.2.2，则需要1.1.1.1服务器防火墙开放8080端口用来让nginx访问到。<br>
如果nginx和要代理应用运行在同机器上则不用另外开启防火墙。例如：nginx代理127.0.0.1:8080，不需要额外开放8080端口。