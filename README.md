# 進入資料庫
資料庫名稱：laravel
資料庫密碼：laravel
```
docker-compose exec db bash
mysql -u root -p
Password: laravel
```


重新載入設定
```
FLUSH PRIVILEGES;
```

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