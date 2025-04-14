# avocado_docker
Docker enviroment

to make it on production
uncomment expose for frontend in docker-compose.yml

comment dev part in frontend/Dockerfile
uncomment prod part in frontend/Dockerfile

change server.host in vite.config.js

change server_name in nginx/default.conf

run (both production фтв вум)
docker-compose build
docker-compose up -d
