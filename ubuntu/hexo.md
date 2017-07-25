# install
`npm install -g hexo-cli`
# init
`hexo init blog`
# change style
1. find style github
2. cd init folder
3. git clone
4. change config file `_config.yml`

# with nginx
```
server {
        listen 80;
        server_name yout_domain;
        access_log  /var/log/nginx/Blog-access.log;
        error_log  /var/log/nginx/Blog-error.log;

        root /home/sanborn/blog/public;
        location / {
            index  index.html index.htm;
        }

}
~

```
