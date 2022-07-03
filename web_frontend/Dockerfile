FROM node:lts AS development

WORKDIR /code
COPY rateam_alt/package.json rateam_alt/package-lock.json /code/
RUN npm ci
COPY ./rateam_alt /code/
CMD ["npm", "start"]

FROM development AS builder
RUN npm run build

FROM nginx:alpine
COPY --from=builder /code/build /usr/share/nginx/html
