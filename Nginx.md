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
在http中添加
`limit_req_zone $binary_remote_addr zone=ipLimit:10m rate=150r/s;`
在 location中添加
`limit_req zone=ipLimit burst=150 nodelay;`
# 缓存
## http 中添加
```
proxy_connect_timeout 5;  
proxy_read_timeout 60;  
proxy_send_timeout 5;  
proxy_buffer_size 16k;  
proxy_buffers 4 64k;  
proxy_busy_buffers_size 128k;  
proxy_temp_file_write_size 128k;  
proxy_temp_path /home/xxx/temp;  
proxy_cache_path /home/xxx/cache levels=1:2 keys_zone=cache_on:50m inactive=20m max_size=10g;  
```
## location中
```
proxy_cache cache_on;  
proxy_cache_valid any 1h;  # any 可以缓存任意的 res

proxy_cache_key $host$uri$is_args$args;  
proxy_pass  http://xxx.xxx.com;
proxy_ignore_headers "Cache-Control" "Expires" "Set-Cookie"; #忽略服务器中使用的 
expires 30d;   
proxy_set_header Host $host;  
proxy_set_header X-Real-IP $remote_addr;  
proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;  
add_header X-Cache-Status $upstream_cache_status; #在response header中添加缓存命中状态
```

## Ref
http://nginx.org/en/docs/http/ngx_http_proxy_module.html?&_ga=1.179671140.1192180146.1425500797#proxy_cache_valid
