# avocado_docker
Docker enviroment

to make it on production
uncomment expose for frontend in docker-compose.yml

comment dev part in frontend/Dockerfile
uncomment prod part in frontend/Dockerfile

change server.host in vite.config.js

change server_name in nginx/default.conf

run (both production and dev)
docker-compose build
docker-compose up -d

for dev development do `npm run dev` in vue repo, but open frontend on avocado.test (server_name from default.conf in main nginx) - not on the url from vite output