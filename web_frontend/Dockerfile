FROM node:lts AS development

WORKDIR /code
COPY ./rateam_alt /code/
RUN npm ci
CMD ["npm", "start"]

FROM development AS builder
RUN npm run build

FROM nginx:alpine
COPY --from=builder /code/build /usr/share/nginx/html
