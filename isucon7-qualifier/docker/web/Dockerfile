FROM alpine AS build-dev

ARG GIT_URL=https://github.com/kouheiszk/isucon7-qualify.git

RUN \
  apk --no-cache add git && \
  git clone --depth=1 $GIT_URL /isubata && \
  rm -rf /isubata/.git

FROM nginx:1.10

COPY --from=build-dev /isubata /home/isucon/isubata
#COPY --from=build-dev /isubata/files/app/nginx.conf /etc/nginx/conf.d/isucon.conf
COPY nginx.conf /etc/nginx/nginx.conf
COPY isucon.conf /etc/nginx/conf.d/isucon.conf
RUN \
  apt-get update && \
  apt-get install -y wget unzip
RUN \
  cd /tmp && \
  wget https://github.com/tkuchiki/alp/releases/download/v1.0.3/alp_linux_s390x.zip && \
  unzip alp_linux_s390x.zip && \
  install alp /usr/local/bin/alp
RUN \
  rm -f /var/log/nginx/access.log && \
  rm -f /var/log/nginx/error.log
