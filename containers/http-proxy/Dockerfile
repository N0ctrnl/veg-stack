FROM nginx:1.11.9-alpine

# for htpasswd command
RUN apk add --no-cache --update apache2-utils
RUN rm -f /etc/nginx/conf.d/*

ENV EDITOR_SERVER_NAME edit.gilpin.info
ENV SPIRE_SERVER_NAME spire.gilpin.info
ENV EDITOR_PORT 80
ENV SPIRE_PORT 81
ENV CLIENT_MAX_BODY_SIZE 1m
ENV PROXY_READ_TIMEOUT 60s
ENV WORKER_PROCESSES 1

COPY files/run.sh /
COPY files/nginx.conf.tmpl /
COPY files/cert.cer /
COPY files/cert.key /

RUN chmod +x /run.sh

# use SIGQUIT for graceful shutdown
# c.f. http://nginx.org/en/docs/control.html
STOPSIGNAL SIGQUIT

ENTRYPOINT ["/run.sh"]
