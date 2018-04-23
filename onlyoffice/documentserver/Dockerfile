FROM onlyoffice/documentserver:5.1.2.9
LABEL maintainer="fcwu.tw@gmail.com"

RUN curl -sSL https://www.rabbitmq.com/rabbitmq-release-signing-key.asc | apt-key add - \
    && echo "deb http://www.rabbitmq.com/debian testing main" > /etc/apt/sources.list.d/rabbitmq.list \
    && curl -sSL https://packages.erlang-solutions.com/debian/erlang_solutions.asc | apt-key add - \
    && echo "deb http://packages.erlang-solutions.com/debian jessie contrib" > /etc/apt/sources.list.d/erlang.list \
    # rabbitmq ipv6
    && apt-get update \
    && apt-get install -y erlang-base-hipe \
    && apt-get install -y rabbitmq-server \
    # CJK fonts
    && apt-get install -y fonts-wqy-microhei fonts-wqy-zenhei \
    && rm -rf /var/lib/apt/lists/* \
    # nginx ipv6
    && sed -i s/localhost/127.0.0.1/ /etc/nginx/includes/* \
    && sed -i '/listen \[::\]:80 default_server;/d' /etc/nginx/conf.d/* \
    # CJK fonts
    && fc-cache -fv \
    && documentserver-generate-allfonts.sh

ADD root /
