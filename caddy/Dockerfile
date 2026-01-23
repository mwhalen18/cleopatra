ARG CADDY_VERSION=2.10.0

FROM caddy:${CADDY_VERSION}-builder AS builder

RUN xcaddy build \
    --with github.com/caddy-dns/porkbun

FROM caddy:${CADDY_VERSION}-alpine
RUN apk add --no-cache tzdata curl

COPY --from=builder /usr/bin/caddy /usr/bin/caddy