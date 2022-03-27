# build environment
FROM node:12-alpine
WORKDIR /usr/app/front
EXPOSE 3000
COPY ./ ./
RUN npm install
ENTRYPOINT ["npm", "start"]