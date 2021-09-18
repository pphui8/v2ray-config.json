## https://blog.dbnuo.com/20191030/ztkytl.html
## https://blog.csdn.net/wudinaniya/article/details/103284695

```json
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

        ssl_ciphers HIGH:!aNULL:!MD5;
        ssl_prefer_server_ciphers on;

        if ($ssl_protocol = "") { 
            return 403;
        }

        location /ray {
            proxy_pass       http://127.0.0.1:7789;
            proxy_redirect             off;
            proxy_http_version         1.1;
            proxy_set_header Upgrade   $http_upgrade;
            proxy_set_header Connection "upgrade";
            proxy_set_header Host      $http_host;
        }

        location / {
            root /data/www/;
            index index.html;
        }

        error_page 404 403 400 500 502 503 504  /error.html;
        location = /data/www/error/index.html {
            root html;
        }
    }
```
