# build environment
FROM node:12-alpine AS base
RUN mkdir -p /home/node/app
RUN chown -R node:node /home/node && chmod -R 770 /home/node
WORKDIR /home/node/app

FROM base AS builder-server
WORKDIR /home/node/app
RUN apk add --no-cache --virtual .build-deps \
    git \
    g++ \
    make

COPY --chown=node:node ./frontend .
USER node

RUN npm install --loglevel warn && npm run build

FROM base AS production
WORKDIR /home/node/app
USER node
COPY --chown=node:node --from=builder-server /home/node/app/ .
EXPOSE 3000

CMD ["npm", "start"]