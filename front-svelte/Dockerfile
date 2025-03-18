# docker build --no-cache -t front-sv . && docker run -p 3000:3000 front-sv
FROM node:latest as build
WORKDIR /app
RUN git clone https://github.com/ndudnicz/front-stocks-svelte.git front
WORKDIR /app/front
RUN npm ci
COPY . .
RUN npm run build
RUN npm prune --production

FROM node:22-alpine
WORKDIR /app
COPY --from=build /app/front/build build/
COPY --from=build /app/front/node_modules node_modules/
EXPOSE 3000
ENV NODE_ENV=production
CMD [ "node", "build" ]