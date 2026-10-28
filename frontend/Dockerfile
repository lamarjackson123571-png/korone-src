FROM node:20-alpine

WORKDIR /app

COPY package.json package-lock.json ./
RUN npm ci

COPY . .

# Pass the database variable into the build arguments so Next.js can read it
ARG DATABASE_URL
ENV DATABASE_URL=$DATABASE_URL

ARG FRONTEND_CONFIG=config.docker-prod.json
RUN cp "$FRONTEND_CONFIG" config.json && npm run build

ENV NODE_ENV=production
ENV PORT=3000

EXPOSE 3000

CMD ["npm", "run", "start"]
