# Build Stage
FROM node:20 as build-stage

WORKDIR /app

# Copier les fichiers package.json et package-lock.json
COPY package*.json ./

# Installer les dépendances
RUN npm install

# Copier le reste des fichiers
COPY . .

# Build du projet Angular
RUN npm run build --prod

# Production Stage
FROM nginx:alpine

COPY --from=build-stage /app/dist/frontend /usr/share/nginx/html

# Exposer le port
EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
