# build environment
FROM node:12-alpine AS base
RUN mkdir -p /usr/src/app
RUN chown -R node:node /home/node && chmod -R 770 /home/node
WORKDIR /usr/src/app

FROM base AS builder-server
WORKDIR /usr/src/app
RUN apk add --no-cache --virtual .build-deps \
    git \
    g++ \
    make

COPY ["frontend/package-lock.json", "frontend/package-lock.json*", "./"]
RUN chown -R node /usr/src/app
USER node

RUN npm install --production --silent && mv node_modules ../

FROM base AS production
ENV NODE_ENV=production
WORKDIR /usr/src/app
USER node
COPY --chown=node:node --from=builder-server ./usr/src/app/ ./usr/src/app

EXPOSE 3000

CMD ["npm", "start"]