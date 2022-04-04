# build environment
FROM node:12-alpine AS base
RUN mkdir -p /usr/src/app
RUN chown -R node:node /usr/src/app && chmod -R 770 /usr/src/app
WORKDIR /usr/src/app

FROM base AS builder-server
WORKDIR /usr/src/app
RUN apk add --no-cache --virtual .build-deps \
    git \
    g++ \
    make

COPY --chown=node:node ./frontend .
# COPY --chown=node:node ./node_modules .

USER node

RUN npm install --loglevel warn && npm run build

FROM base AS production
WORKDIR /usr/src/app
USER node
COPY --chown=node:node --from=builder-server /usr/src/app/ /usr/src/app

EXPOSE 3000

CMD ["npm", "start"]