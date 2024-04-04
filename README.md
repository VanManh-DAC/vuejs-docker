# vuejs-docker
1. docker-compose build -d 


---------------------
"8089:8080" => chuyển cổng 8080 thành 8089 


---------------------
FROM node:lts-alpine as develop-stage
WORKDIR /app
COPY package*.json ./
RUN npm install
RUN npm install axios  <== cài thư viện 
COPY . .
CMD ["npm", "run", "start"]   
FROM develop-stage as build-stage
RUN npm run build
FROM nginx:latest as production-stage
COPY --from=build-stage /app/dist /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
---------------------
