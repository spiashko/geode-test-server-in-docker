FROM apachegeode/geode
RUN apk add --update \
    curl \
    && rm -rf /var/cache/apk/*

ENV SERVER_NAME server
ENV LOCATOR_NAME locator

ADD aliases.sh /etc/profile.d/aliases.sh

COPY cache.xml /geode/config/cache.xml
CMD CONTAINER_IP="$(hostname -i)" && \
gfsh start locator --name=$LOCATOR_NAME  && \
gfsh start server --name=$SERVER_NAME --start-rest-api=true --http-service-port=8080 --http-service-bind-address=$CONTAINER_IP --cache-xml-file=/geode/config/cache.xml --J=-Xdebug --J=\"-Xrunjdwp:transport=dt_socket,server=y,suspend=n,address=5005\" && \
bash -l
