# Utiliser une image de base appropriée
FROM node:16-alpine as builder

# Définissez le répertoire de travail sur /app à l'intérieur du conteneur
WORKDIR /app

# Copier les fichiers d'application
COPY . .

# Installer les dépendances (npm ci s'assure que les versions exactes du fichier de verrouillage sont installées)
RUN npm ci 

# Créer l'application
RUN npm run build

# Regroupez les actifs statiques avec nginx
FROM nginx:1.21.0-alpine as production

ENV NODE_ENV production

# Copier les ressources créées à partir de l'image "builder"
COPY --from=builder /app/build /usr/share/nginx/html

# Ajout de notre nginx.conf
COPY ./nginx/nginx.conf /etc/nginx/conf.d/default.conf

# Expose port
EXPOSE 80

# Commencer nginx
CMD ["nginx", "-g", "daemon off;"]
