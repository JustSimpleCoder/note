phpbrew.md

vi /Users/xxxx/.phpbrew/php/php-7.1.31/etc/php-fpm.conf


vi /Users/xxxx/.phpbrew/php/php-7.1.31/etc/php-fpm.d/www.conf




vi /Users/xxxx/.phpbrew/php/php-7.1.31/etc/php-fpm.d/www.conf

listen = 127.0.0.1:9000

Installing shared extensions:     /Users/yaobin/.phpbrew/php/php-7.3.8/lib/php/extensions/no-debug-non-zts-20180731/
Installing header files:          /Users/yaobin/.phpbrew/php/php-7.3.8/include/php/



```
NG
server {
        listen       80;
        server_name  bs.x bs.dev.staff.xdf.cn ;
        #testwxadmin.staff.xdf.cn;
        index        index.html index.htm index.php;
        root         /Users/xxxx/Project/XDF/backend-service/public;
        access_log  /var/log/nginx/access.log ;

       add_header Access-Control-Allow-Origin *;
       add_header Access-Control-Allow-Credentials true;
       add_header Access-Control-Allow-Headers "Origin, Content-Type, Cookie, X-CSRF-TOKEN, Accept, Authorization, X-XSRF-TOKEN";
       add_header Access-Control-Allow-Methods *;

        if (!-e $request_filename) {
                rewrite ^/(.+)$ /index.php/$1 last;
                break;
        }

         location ~ .*\.php {
            #fastcgi_pass  unix:/tmp/php-cgi.sock;
            if ($request_filename ~* (.*)\.php) {
                set $php_url $1;
            }
            if (!-e $php_url.php) {
                return 404;
            }

            fastcgi_pass        127.0.0.1:9000;
           # fastcgi_pass       unix:/Users/yaobin/.phpbrew/php/php-7.1.31/var/run/php-fpm.pid;
            fastcgi_index       index.php;
            include             fastcgi_params;
            fastcgi_split_path_info ^(.+\.php)(.*)$;
            fastcgi_param   PATH_INFO               $fastcgi_path_info;
            fastcgi_param   PATH_TRANSLATED $document_root$fastcgi_path_info;
            fastcgi_param   SCRIPT_FILENAME $document_root$fastcgi_script_name;

        }

          location ~ .*\.(gif|jpg|jpeg|png|bmp|swf)$ {
            expires      30d;
        }

        location ~ .*\.(js|css)?$ {
            expires      1h;
        }
        error_page   500 502 503 504  /50x.html;
        location = /50x.html {
            root   /usr/share/nginx/html;
        }
        error_page 404 /404.html;
        location ~ /(\.ht|\.git|\.svn) {
            deny  all;
        }

    }
````