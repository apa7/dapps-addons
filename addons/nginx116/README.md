## 配置信息

服务端口：80/443

## 说明
1. 查看容器：```$ docker container ls```
2. 进入容器：
   ```
    docker exec -it dapps-nginx116 /bin/sh

    # 查看信息
    nginx -v
   ```

### 配置数目

1. 代码目录为：./dapps/docker/www
2. 配置文件：./dapps/docker/nginx116/config
3. service配置举例：
   ```
    server {
        listen 80;
        charset utf-8;
        server_name 192.168.10.11 local.com;
        root /data/www/test/shop/public;
        index index.html index.htm index.php index.shtml;
        if (!-e $request_filename){
            rewrite ^/(.*)$ /index.php?s=/$1 last;
            break;
        }

        location ~ \.php$ {
            # docker
            root /var/www/html/test/shop/public;
            fastcgi_pass 本机ip:9000; # 或者：127.0.0.1:9000 或者：php72:9000 或者：dapps-php72:9000
            #fastcgi_param  SCRIPT_FILENAME  $document_root$fastcgi_script_name;

            #fastcgi_pass unix:/dev/shm/php-cgi.sock;
            fastcgi_index  index.php;
            include fastcgi.conf;
        }
    }
   ```