FROM node:20-alpine

WORKDIR /app

ENV NODE_ENV=production \
    PORT=3001


RUN addgroup -g 1001 -S nodejs && \
    adduser  -S nodejs -u 1001
    

COPY ./package.json ./
RUN npm install --production

LABEL maintainer="Eng. Abdelhamed" \
      description=" Node.js application" \
      version="1.0"


COPY --chown=nodejs:nodejs ./server.js  ./


EXPOSE 3001

USER nodejs

CMD ["node", "server.js"]