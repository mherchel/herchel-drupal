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

## Clear cache on remote
```
php ./vendor/drush/drush/drush cr
```
