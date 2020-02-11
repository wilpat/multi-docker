FROM node:alpine as builder

WORKDIR '/app'

COPY package.json .

RUN npm i

COPY . .

RUN npm run build

FROM nginx
EXPOSE 3000 
# Traffic here is directed from a parent nginx container that's targeting the port 3000
# So we used 3000 here so elastic beanstalk can direct traffic to the right port
COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf
COPY --from=builder /app/build /usr/share/nginx/html

#No need to specify a command to start nginx as it gets started by default when a container with the image starts