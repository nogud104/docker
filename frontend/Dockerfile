FROM node:lts-alpine AS build
ENV NODE_ENV=production
WORKDIR /usr/src/app
COPY ["package.json", "package-lock.json*", "./"]
RUN npm install --production --silent && mv node_modules ../ 

COPY . .
RUN npm run build


FROM build AS production
WORKDIR /usr/src/app
USER node
COPY --chown=node:node --from=build . .

EXPOSE 3000

ENTRYPOINT ["npm", "start"]
