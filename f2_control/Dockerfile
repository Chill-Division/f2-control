ARG BUILD_FROM
FROM ${BUILD_FROM}

# nginx serves the static crop-steering web UI on port 8420 (exposed via HA ingress)
RUN apk add --no-cache nginx \
    && rm -rf /var/cache/apk/* /etc/nginx/http.d/*

RUN pip3 install --no-cache-dir requests

# vendored: the pure engine package + the IO-shell controller
COPY f2_control /app
WORKDIR /app

# web UI: nginx.conf, the nginx s6 service, and the static pages served from /www/public
COPY files/general /

COPY run.sh /run.sh
RUN chmod a+x /run.sh

CMD [ "/run.sh" ]
