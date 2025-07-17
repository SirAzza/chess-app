# Usa imagen node para construir
FROM node:20-alpine as build

WORKDIR /app

COPY package.json yarn.lock ./

RUN yarn install

COPY . .

RUN yarn build

# Usa una imagen nginx para servir el build estático
FROM nginx:alpine

COPY --from=build /app/build /usr/share/nginx/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
