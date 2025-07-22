# Multi-stage build
FROM node:18-alpine AS builder

WORKDIR /app

# Copier package.json et package-lock.json
COPY package*.json ./

# Installer les dépendances
RUN npm ci

# Copier le code source
COPY . .

# Build de l'application
RUN npm run build

# Image de production avec Nginx
FROM nginx:alpine

# Copier les fichiers buildés
COPY --from=builder /app/dist /usr/share/nginx/html

# Configuration Nginx pour écouter sur le port 4020
RUN echo 'server { \
    listen 4020; \
    server_name localhost; \
    location / { \
        root /usr/share/nginx/html; \
        index index.html index.htm; \
        try_files $uri $uri/ /index.html; \
    } \
}' > /etc/nginx/conf.d/default.conf

# Supprimer la configuration par défaut
RUN rm /etc/nginx/conf.d/default.conf.default 2>/dev/null || true

EXPOSE 4020

HEALTHCHECK --interval=30s --timeout=3s --start-period=10s --retries=3 \
  CMD wget --quiet --tries=1 --spider http://localhost:4020 || exit 1

CMD ["nginx", "-g", "daemon off;"]