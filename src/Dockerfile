FROM node:20-alpine

# tini como PID 1: reenvía SIGTERM a Node para que el contenedor se detenga limpio
RUN apk add --no-cache tini

WORKDIR /app

# Dependencias primero para aprovechar la caché de capas
COPY package*.json ./
RUN npm ci --omit=dev && npm cache clean --force

COPY . .

USER node
EXPOSE 8080

ENTRYPOINT ["/sbin/tini", "--"]
CMD ["node", "server.js"]
