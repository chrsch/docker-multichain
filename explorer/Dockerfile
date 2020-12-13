FROM ubuntu:focal

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update \
        && apt-get upgrade -q -y \
        && apt-get dist-upgrade -q -y \
        && apt-get install -q -y build-essential wget curl xxd python python-dev sqlite3 libsqlite3-dev \
        && curl -O https://raw.githubusercontent.com/pypa/get-pip/master/get-pip.py \
        && python2 get-pip.py \
        && pip install pycrypto \
        && pip install py-ubjson \
        && apt-get clean \
        && rm -rf /var/lib/apt/lists/* \
        && cd /tmp \
        && wget https://www.multichain.com/download/multichain-2.1.1.tar.gz \
        && tar -xvzf multichain-2.1.1.tar.gz \
        && cd multichain-2.1.1 \
        && mv multichaind multichain-cli multichain-util /usr/local/bin \
        && cd /tmp \
        && rm -Rf multichain*

RUN cd /root \
    && wget https://github.com/MultiChain/multichain-explorer/archive/master.tar.gz \
    && tar -xvzf master.tar.gz \
    && rm -Rf master.tar.gz

RUN cd /root/multichain-explorer-master \
    && python setup.py install --user

ADD ./runexplorer.sh /root/runexplorer.sh
RUN chmod a+x /root/runexplorer.sh

EXPOSE 2750

CMD ["/bin/bash", "/root/runexplorer.sh"]
