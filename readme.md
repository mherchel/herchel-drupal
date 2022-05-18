## Push to fortrabbit
```
git push fortrabbit main
```

## Upload database
1. Establish SSH tunnel
```
ssh -N -L 13306:herchel.mysql.us1.frbit.com:3306 herchel@tunnel.us1.frbit.com
```
2. dump the current db
```
drush sql-dump > herchel.sql
```
3. move data over
```
mysql -u herchel -p -h127.0.0.1 -P13306 -Dherchel < ./herchel.sql
```

## Pull down db
1. Establish SSH tunnel
```
ssh -N -L 13306:herchel.mysql.us1.frbit.com:3306 herchel@tunnel.us1.frbit.com
```
2. dump the live db
```
mysqldump --no-tablespaces --user herchel -h 127.0.0.1 --port 13306 --password herchel > dump.sql

```
3. Import data on local
```
mysql -uroot -proot herchel < dump.sql
```
4. Search and replace (because host is running MySQL 8, which MAMP doesn't yet support)
Replace `utf8mb4_0900_ai_ci` with `utf8mb4_general_ci`

## Clear cache on remote
```
php ./vendor/drush/drush/drush cr
```
