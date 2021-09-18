## https://blog.dbnuo.com/20191030/ztkytl.html
## https://blog.csdn.net/wudinaniya/article/details/103284695
turn off SElinux  
```setsebool -P httpd_can_network_connect 1```
```conf
server {
        listen 443 ssl;
        server_name pphui8.me;

        ssl_certificate /etc/letsencrypt/live/pphui8.me/fullchain.pem;
        ssl_certificate_key /etc/letsencrypt/live/pphui8.me/privkey.pem;

        ssl_session_cache shared:ssl:1m;
        ssl_session_timeout 5m;
        ssl_session_cache builtin:1000 shared:SSL:10m;
        ssl_buffer_size 1400;
        add_header Strict-Transport-Security max-age=15768000;
        ssl_stapling on;
        ssl_stapling_verify on;
        server_name pphui8.me;
        ssl_protocols TLSv1 TLSv1.1 TLSv1.2;

        ssl_ciphers HIGH:!aNULL:!MD5;
        ssl_prefer_server_ciphers on;

        if ($ssl_protocol = "") { 
            return 403;
        }

        location / {
            root /data/www/;
            index index.html;
        }

        location /ray { # 与 V2Ray 配置中的 path 保持一致
            proxy_redirect off;
            proxy_pass http://127.0.0.1:7789;#假设WebSocket监听在环回地址的10000端口上
            proxy_http_version 1.1;
            proxy_set_header Upgrade $http_upgrade;
            proxy_set_header Connection "upgrade";
            proxy_set_header Host $http_host;

            # Show realip in v2ray access.log
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        }

        error_page 404 403 400 500 502 503 504  /error.html;
        location = /data/www/error/index.html {
            root html;
        }
    }
```
