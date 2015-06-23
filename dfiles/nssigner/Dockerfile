FROM ubuntu:15.04
MAINTAINER carlos@xt6.us
WORKDIR /root
# COPY ftp://ftp.isc.org/isc/bind9/9.10.2/bind-9.10.2.tar.gz bind.tar.gz
RUN apt-get update
RUN apt-get install -y wget
RUN apt-get install -y libssl-dev build-essential
RUN wget -q --output-document=bind.tar.gz ftp://ftp.isc.org/isc/bind9/9.10.2/bind-9.10.2.tar.gz
RUN mkdir -p /root/bind
RUN tar xzvf /root/bind.tar.gz -C /root/bind --strip-components=1
WORKDIR /root/bind
RUN ./configure --disable-linux-caps --prefix=/opt/bbsigner
RUN make
RUN make install
COPY named.conf /opt/bbsigner/etc/named.conf
ADD http://www.internic.net/domain/named.root /opt/bbsigner/etc/named.root
EXPOSE 53
# ENTRYPOINT ["./ripeval/rpki-validator.sh", "run"]