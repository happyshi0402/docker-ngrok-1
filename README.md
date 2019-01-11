# DOCKER NGROK IMAGE

## BUILD IMAGE

```linux
git clone https://github.com/happyshi0402/wyk1.git wyk
cd wyk
docker build -t happyshi0402/ngrok .
```

## RUN
* you must mount your folder (E.g `/data/ngrok`) to container `/myfiles`
* if it is the first run, it will generate the binaries file and CA in your floder `/data/ngrok`

```linux
docker run -idt --name ngrok-server \
-v /data/ngrok:/myfiles \
-e DOMAIN='tunnel.happyshi0402.cn' happyshi0402/ngrok /bin/sh /server.sh
```

## nginx config

```nginx
server {
     listen       80;
     server_name   tunnel.happyshi0402.cn *.tunnel.happyshi0402.cn;
     location / {
             proxy_set_header X-Real-IP $remote_addr;
             proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
             proxy_set_header Host $http_host;
             proxy_set_header X-Nginx-Proxy true;
             proxy_set_header Connection "";
             proxy_pass http://172.17.92.158:8085; #服务器内容IP
     }
     access_log /var/logs/admin_ngrok.log;
     error_log  /var/logs/admin_ngrok.error.log;
 }
```

###客户端配置
必须采用docker生成的密钥生成客户端程序才行
