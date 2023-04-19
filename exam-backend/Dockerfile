# l'image officielle Node.js comme image de base
FROM node:14

# Optimiser l'application pour un environnement de production
ENV NODE_ENV=production

# le répertoire de travail dans le conteneur
WORKDIR /app

# Copier package.json et package-lock.json dans /app
COPY ["package.json","package-lock.json" ,"./"]

# Installation des dépendances du projet
RUN npm install --production 

# Copier le reste du code de l'application dans /app
COPY . .

# Le port pour que le backend écoute
EXPOSE 5000

# Démarrage de l'application principale
CMD ["node","server.js"]

