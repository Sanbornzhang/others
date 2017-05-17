# 反向代理
```
location / {
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_pass http://URL;
}
```
# 负载均衡
## base 
```
upstream serveName {   //serveName 在下面会使用到
             server 192.168.3.10;
             server 192.168.3.11;
             server 192.168.3.12;

         }
server {
        listen 80 default_server;
        listen [::]:80 default_server
        server_name _;

        location / {
                proxy_set_header Host $host;
                proxy_set_header X-Real-IP $remote_addr;
                proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
                proxy_pass http://serveName;  //这里会使用到
        }
}
```
## 策略
### 轮询
上面写的是一种 轮询的策略。
当访问到对应的服务时候 回首先访问到  10 下一次请求收到的时候会访问到 11 在下一次是 12 然后再到 10
### 权重
```
upstream serveName { 
  server 192.168.3.10 weight=9; 
  server 192.168.0.11 weight=10; 
} 
```
指定轮询几率，weight和访问比率成正比，用于后端服务器性能不均的情况
###  ip_hash
```
upstream serveName { 
ip_hash; 
    server 192.168.0.10; 
    server 192.168.0.11; 
} 
```

### fair
```
upstream serveName { 
    server 192.168.0.10; 
    server 192.168.0.11; 
    fair; 
} 
```
# IP限制
