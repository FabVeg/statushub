
# Stage 1 : Build
FROM node:26-alpine AS builder

WORKDIR /app

# Installation des dépendances
COPY package*.json ./
RUN npm ci

# Copie du code source
COPY . .

# Compilation NestJS
RUN npm run build


# Stage 2 : Production
FROM node:26-alpine AS production

WORKDIR /app

ENV NODE_ENV=production

# Installation des dépendances de production
COPY package*.json ./
RUN npm ci --omit=dev && npm cache clean --force

# Récupération de l'application compilée
COPY --from=builder /app/dist ./dist

EXPOSE 3000

CMD ["node", "dist/main.js"]
