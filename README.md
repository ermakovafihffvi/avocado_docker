# avocado_docker
Docker enviroment

## to make it on production
uncomment expose for frontend adn db in docker-compose.yml

upd env (APP_URL and DB - DB_HOST - 172.17.0.1)
чтобы узнать адрес 
ip addr show docker0 или ifconfig


comment dev part in frontend/Dockerfile
uncomment prod part in frontend/Dockerfile

change server.host in vite.config.js

change server_name in nginx/default.conf

run (both production and dev)
docker-compose build
docker-compose up -d

//comment on db: чтобы контейнер лары мог обзать с внешней бд
SELECT user, host FROM mysql.user WHERE user = 'root';
CREATE USER 'root'@'%' IDENTIFIED BY __password__;
GRANT ALL PRIVILEGES ON __db_name__.* TO 'root'@'%';
FLUSH PRIVILEGES;

изнутри контейнера с ларой: nc -zv 172.17.0.1 3306
должно быть всё ок, если нет
/etc/mysql/mysql.conf.d/mysqld.cnf (или /etc/my.cnf.d/mysqld.cnf)
bind-address = 0.0.0.0

sudo systemctl restart mysql

проверка из линукса: sudo ss -tlnp | grep 3306 
должна быть строчка 0.0.0.0

если проверка изнутри контйнера nc -zv 172.17.0.1 3306 так и не заработает
из линукса  
sudo ufw status
Если там нет строки вида 3306/tcp ALLOW Anywhere
sudo ufw allow 3306/tcp

## for dev development 
sdo `npm run dev` in vue repo, but open frontend on avocado.test (server_name from default.conf in main nginx) - not on the url from vite output

//TEMP SOLUTION
if after npm run dev you see permissions error do
sudo chown -R $USER:$USER /home/alex/avocado_vue/node_modules


## CRON
enter container as root:
docker-compose exec -u root php-fpm bash

add log file:
touch /var/log/cron-debug.log
chmod 666 /var/log/cron-debug.log

check cron:
service cron status

set cron task:
crontab -e

PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

* * * * * cd /var/www/html && php artisan schedule:run >> /var/log/cron-debug.log 2>&1
