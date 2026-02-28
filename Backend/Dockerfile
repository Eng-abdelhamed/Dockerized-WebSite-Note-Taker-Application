FROM node:20-alpine

WORKDIR /app

ENV NODE_ENV=production \
    PORT=3001
COPY ./package.json ./
RUN npm install --production

LABEL maintainer="Eng. Abdelhamed" \
      description=" Node.js application" \
      version="1.0"

COPY ./server.js .

EXPOSE 3001

CMD ["node", "server.js"]