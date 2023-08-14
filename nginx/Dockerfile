FROM nginx:latest AS base

COPY nginx/assets/etc/nginx /etc/nginx

FROM node:lts-slim AS builder-base

RUN mkdir -p /work/app/

WORKDIR /work/app/
COPY ./package.json /work/app/package.json
RUN yarn install

FROM builder-base AS builder

WORKDIR /work/app/
COPY ./components /work/app/components
COPY ./pages /work/app/pages
RUN yarn run build

FROM base

COPY --from=builder /work/app/out /usr/share/nginx/html/

EXPOSE 80

STOPSIGNAL SIGTERM

CMD ["nginx", "-g", "daemon off;"]
