FROM nginx:latest AS base

COPY nginx/assets/etc/nginx /etc/nginx

FROM node:lts-slim AS builder

RUN npm -g i pnpm

COPY app /work/app
WORKDIR /work/app

RUN pnpm install\
 && pnpm build

FROM base

COPY --from=builder /work/app/out /usr/share/nginx/html/

EXPOSE 80

STOPSIGNAL SIGTERM

CMD ["nginx", "-g", "daemon off;"]
