# Etapa 1: Build del frontend
FROM node:20-alpine AS build

# Establecer directorio de trabajo
WORKDIR /app

# Copiar archivos de definición de dependencias
COPY package.json yarn.lock ./

# Instalar cross-env para poder usar variables NODE_OPTIONS multiplataforma
RUN yarn add cross-env --dev

# Instalar dependencias con yarn
RUN yarn install --frozen-lockfile

# Copiar todo el código fuente
COPY . .

# Construir la app con variable para OpenSSL
RUN npx cross-env NODE_OPTIONS=--openssl-legacy-provider react-scripts build

# Etapa 2: Servir con Nginx
FROM nginx:stable-alpine

# Copiar el build de React a la carpeta que Nginx sirve
COPY --from=build /app/build /usr/share/nginx/html

# Copiar configuración personalizada de nginx si tienes (opcional)
# COPY nginx.conf /etc/nginx/nginx.conf

# Exponer el puerto 80
EXPOSE 80

# Comando para correr nginx en primer plano
CMD ["nginx", "-g", "daemon off;"]