# fluentd/Dockerfile
#FROM fluent/fluentd:v1.9.1-debian-1.0
#User root
#RUN gem install fluent-plugin-elasticsearch
#RUN gem install fluent-plugin-kafka
#User fluent
FROM fluent/fluentd:v1.11-1

# Use root account to use apk
USER root

# below RUN includes plugin as examples elasticsearch is not required
# you may customize including plugins as you wish
RUN apk add --no-cache --update --virtual .build-deps \
        sudo build-base ruby-dev \
 && sudo gem install fluent-plugin-elasticsearch \
 && sudo gem install fluent-plugin-kafka \
 && sudo gem install libgeoip-dev \
 && sudo gem isntall libmaxminddb-dev \
 && sudo gem install fluent-plugin-geoip \

 && sudo gem sources --clear-all \
 && apk del .build-deps \
 && rm -rf /tmp/* /var/tmp/* /usr/lib/ruby/gems/*/cache/*.gem 

#COPY fluent.conf /fluentd/etc/
COPY entrypoint.sh /bin/

USER fluent
