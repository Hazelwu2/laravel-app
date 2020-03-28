# 專案設定步驟

1. 設定Env
```
cp .env.example .env
vi .env
```

.env修改
```
DB_CONNECTION=mysql
DB_HOST=db
DB_PORT=3306
DB_DATABASE=laravel
DB_USERNAME=laravel
DB_PASSWORD=laravel
```

2. 啟動Docker
```
docker-compose up -d
```

3. 在mysql授予權限
```
docker-compose exec db bash
root@c31b7b3251e0:/# mysql -u root -p
```
進入mysql介面後，先叫出資料庫
並自行修改laravel
```
mysql>show databases;
mysql>GRANT ALL ON laravel.* TO 'laravel'@'%' IDENTIFIED BY 'your_laravel_db_password';
```

輸入完後重新載入設定
```
mysql>FLUSH PRIVILEGES;
mysql> EXIT;
```

## 跑Migrate

```
docker-compose exec app php artisan migrate
```
成功會出現 Output
```
Migration table created successfully.
Migrating: 2014_10_12_000000_create_users_table
Migrated:  2014_10_12_000000_create_users_table
Migrating: 2014_10_12_100000_create_password_resets_table
Migrated:  2014_10_12_100000_create_password_resets_table
```


## 設定Nginx
```
cd /laravel-app/nginx/conf.d
vi  app.conf
```
預設Nginx App.conf
```
server {
    listen 80;
    index index.php index.html;
    error_log  /var/log/nginx/error.log;
    access_log /var/log/nginx/access.log;
    root /var/www/public;
    location ~ \.php$ {
        try_files $uri =404;
        fastcgi_split_path_info ^(.+\.php)(/.+)$;
        fastcgi_pass app:9000;
        fastcgi_index index.php;
        include fastcgi_params;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        fastcgi_param PATH_INFO $fastcgi_path_info;
    }
    location / {
        try_files $uri $uri/ /index.php?$query_string;
        gzip_static on;
    }
}
```




