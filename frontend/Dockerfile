# Stage 1: Build Angular app
FROM node:14 AS builder

WORKDIR /app

COPY ./package*.json ./

RUN npm install

COPY . .

RUN npm run build -- --output-path=dist/app


# Stage 2: Nginx to maintain static
FROM nginx:alpine

RUN rm /etc/nginx/conf.d/default.conf

COPY ./nginx.tmpl /etc/nginx/templates/default.conf.template

COPY --from=builder /app/dist/app /usr/share/nginx/html

EXPOSE 80
