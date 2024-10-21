# Utiliser l'image Node.js officielle pour construire
FROM node:18 AS builder
WORKDIR /app

# Copier les fichiers package et installer les dépendances
COPY package*.json ./
RUN npm install

# Copier le reste du code source et construire l'application
COPY . .
RUN npm run build

# Utiliser une image plus légère pour servir l'application
FROM node:18-alpine
WORKDIR /app
COPY --from=builder /app ./

# Définir la variable d'environnement
ENV NEXT_PUBLIC_API_BASE_URL=http://api:8000

# Exposer le port sur lequel l'application fonctionne
EXPOSE 3000
CMD ["npm", "start"]
