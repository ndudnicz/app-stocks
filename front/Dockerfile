# docker build --no-cache -t front . && docker run -p 4200:80 front
FROM node:latest as build

WORKDIR /app
RUN git clone https://github.com/ndudnicz/front-stocks.git front
WORKDIR /app/front
RUN npm install
RUN npm run build

FROM nginx:latest

COPY --from=build /app/front/dist/front/browser /usr/share/nginx/html
EXPOSE 80