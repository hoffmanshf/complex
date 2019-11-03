FROM node:alpine as builder
# build phase is to install the dependencies and build the application
WORKDIR /app
COPY ["package.json", "package-lock.json*", "npm-shrinkwrap.json*", "./"]
RUN npm install

COPY . .
RUN npm run build

# run phase
FROM nginx
EXPOSE 3000
COPY ["./nginx/default.conf", "/etc/nginx/conf.d/default.conf"]
# copy the production build assets from build phase
COPY --from=builder /app/build /usr/share/nginx/html
# we don't need to specifically run start nginx