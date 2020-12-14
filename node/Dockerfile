FROM ubuntu:focal

ENV DEBIAN_FRONTEND noninteractive

ENV TZ=Europe/Berlin
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN apt-get update \
        && apt-get upgrade -q -y \
        && apt-get dist-upgrade -q -y \
        && apt-get install -q -y wget curl xxd tzdata \
        && apt-get clean \
        && rm -rf /var/lib/apt/lists/* \
        && cd /tmp \
        && wget https://www.multichain.com/download/multichain-2.1.1.tar.gz \
        && tar -xvzf multichain-2.1.1.tar.gz \
        && cd multichain-2.1.1 \
        && mv multichaind multichain-cli multichain-util /usr/local/bin \
        && cd /tmp \
        && rm -Rf multichain*
ADD ./runchain.sh /root/runchain.sh
RUN chmod a+x /root/runchain.sh

CMD ["/bin/bash", "/root/runchain.sh"]
