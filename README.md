# avocado_docker
Docker enviroment

## to make it on production
uncomment expose for frontend in docker-compose.yml

comment dev part in frontend/Dockerfile
uncomment prod part in frontend/Dockerfile

change server.host in vite.config.js

change server_name in nginx/default.conf

run (both production and dev)
docker-compose build
docker-compose up -d

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
