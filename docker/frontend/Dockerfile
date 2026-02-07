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
RUN npm run build

# Production Stage
FROM nginx:alpine

# Copier la configuration nginx
COPY ./nginx.conf /etc/nginx/nginx.conf

# Copier les fichiers buildés (Angular 18+ utilise /browser)
COPY --from=build-stage /app/dist/frontend/browser /usr/share/nginx/html

# Exposer le port
EXPOSE 80

# Démarrer nginx
CMD ["nginx", "-g", "daemon off;"]