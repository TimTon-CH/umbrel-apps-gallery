FROM node:20-bookworm-slim AS builder

WORKDIR /build
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

FROM node:20-bookworm-slim

WORKDIR /app
RUN mkdir -p /app/data && chown -R node:node /app
USER node

COPY --from=builder /build/dist ./dist
COPY --from=builder /build/node_modules ./node_modules
COPY --from=builder /build/package.json ./

EXPOSE 3333 3335

CMD ["node", "dist/main.js"]
