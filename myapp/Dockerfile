ARG BUILD_FROM
FROM $BUILD_FROM


# Copy root filesystem
# COPY rootfs /

# Setup requirements
ARG BUILD_ARCH
env BUILD_ARCH $BUILD_ARCH

# RUN set -x \
#     && apk add --no-cache curl \
#     && if [[ "${BUILD_ARCH}" = "aarch64" ]]; then ARCH="arm64"; fi \
#     && if [[ "${BUILD_ARCH}" = "amd64" ]]; then ARCH="amd64"; fi \
#     && if [[ "${BUILD_ARCH}" = "armhf" ]]; then ARCH="arm"; fi \
#     && if [[ "${BUILD_ARCH}" = "armv7" ]]; then ARCH="arm"; fi \
#     && if [[ "${BUILD_ARCH}" = "i386" ]]; then ARCH="386"; fi
# RUN apk add --no-cache openssh file libc6-compat
# RUN ssh-keygen -b 2048 -t rsa -f /root/.ssh/id_rsa -q -N ""

# COPY run.sh /
# RUN chmod a+x /run.sh
# CMD [ "/run.sh" ]


# FROM node:lts-alpine AS builder
# WORKDIR /app
# COPY . ./
# COPY .env.dev ./.env
# RUN npm install && npm run build

FROM nginx:alpine
COPY nginx.conf /etc/nginx/conf.d/configfile.template
#COPY --from=builder /app/build /usr/share/nginx/html
ENV PORT=8080 HOST=0.0.0.0
EXPOSE 8080
CMD sh -c "envsubst '\$PORT' < /etc/nginx/conf.d/configfile.template > /etc/nginx/conf.d/default.conf && nginx -g 'daemon off;'"
