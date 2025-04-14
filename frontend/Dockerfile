#prod
#FROM node:22 as build-stage
#WORKDIR /app
#COPY package*.json ./
#RUN npm install
#COPY ./ .
#RUN npm run build

#FROM nginx as production-stage
#EXPOSE 3000
#COPY nginx.conf /etc/nginx/conf.d/default.conf
#COPY --from=build-stage /app/dist /usr/share/nginx/html
#CMD ["nginx", "-g", "daemon off;"]

#dev
FROM node:22

WORKDIR /app

COPY package*.json ./
RUN npm install

COPY ./ .

EXPOSE 3000

CMD ["npm", "run", "dev"]