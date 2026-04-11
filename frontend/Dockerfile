FROM dhi.io/node:24-debian13-dev AS build

WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .
RUN npm run build

FROM dhi.io/node:24-debian13 AS production

WORKDIR /app
ENV NODE_ENV=production

COPY --from=build /app/.output /app/.output
COPY --from=build /app/package.json /app/package.json

EXPOSE 3000

CMD [ "node", ".output/server/index.mjs" ]
