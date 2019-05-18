FROM ubuntu:18.04

WORKDIR /var/submariner

COPY strongswan*.tar.gz /var/tmp

RUN echo 'debconf debconf/frontend select Noninteractive' | debconf-set-selections && apt-get -y update && apt-get -y install curl iproute2 iptables libatm1 libgmp10 libmnl0 libnfnetlink0 libssl1.0.0 iptables-nftables-compat

RUN /bin/bash -c "cd / && cp /var/tmp/strongswan*.tar.gz . && tar -zxvf strongswan*.tar.gz && rm strongswan*.tar.gz"

COPY charon.conf /usr/local/etc/strongswan.d/charon.conf
COPY submariner.sh /usr/local/bin

RUN chmod +x /usr/local/bin/submariner.sh

RUN rm -f /sbin/iptables && ln -s xtables-compat-multi /sbin/iptables

COPY submariner-engine /usr/local/bin

# temporary sleep infinity so that we can do our debugging
ENTRYPOINT submariner.sh
