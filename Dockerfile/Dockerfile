FROM ubuntu:18.04
#ENV container docker
## Install Suricata as describe here https://redmine.openinfosecfoundation.org/projects/suricata/wiki/CentOS_Installation
RUN apt-get update
RUN apt -y install libpcre3 libpcre3-dev build-essential autoconf wget apt-utils \
    automake libtool libpcap-dev libnet1-dev libyaml-0-2 libyaml-dev liblua5.1-dev \
    zlib1g zlib1g-dev libmagic-dev libcap-ng-dev libjansson-dev pkg-config \
    libnetfilter-queue-dev geoip-bin geoip-database geoipupdate apt-transport-https

RUN cd /tmp/ \
    && wget https://www.openinfosecfoundation.org/download/suricata-4.1.2.tar.gz \
    && tar -xvzf /tmp/suricata-4.1.2.tar.gz 
RUN cd /tmp/suricata-4.1.2/ \
    && ./configure --prefix=/usr --sysconfdir=/etc --localstatedir=/var --enable-nfqueue --enable-lua \
    --disable-suricata-update --enable-ebpf --enable-ebpf-build
RUN cd /tmp/suricata-4.1.2/ \
    && make \
    && make install-full\
    && ldconfig
# Install Suricata-update utility https://github.com/OISF/suricata-update
RUN apt -y install python-pip python-yaml
RUN pip install --pre --upgrade suricata-update
#RUN apt install -y cronie
#COPY suricata-update.sh /etc/suricata/suricata-update.sh
# COPY file needed for the Suricata efficiency
#RUN apt install -y cronie
#COPY suricata-update-cron /etc/cron.d/suricata-update-cron
#RUN chmod +x /etc/cron.d/suricata-update-cron
#COPY docker-entrypoint.sh /tmp/docker-entrypoint.sh
#RUN chmod +x /tmp/docker-entrypoint.sh
#COPY suricata.yaml /etc/suricata/suricata.yaml


