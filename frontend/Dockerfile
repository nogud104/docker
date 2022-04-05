FROM node:lts-alpine AS build
ENV NODE_ENV=production
WORKDIR /usr/src/app
COPY ["package*.json", "./"]
RUN npm install --production && mv node_modules ../
COPY . .
RUN npm run build

FROM build AS production
WORKDIR /usr/src/app
COPY --chown=node:node --from=build . .
RUN npm install -g serve
EXPOSE 3000
USER node
CMD ["serve", "-s", "build"]