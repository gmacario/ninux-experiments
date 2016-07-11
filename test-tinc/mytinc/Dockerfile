# test-tinc/mytinc/Dockerfile

FROM ubuntu:16.04
MAINTAINER Gianpaolo Macario <gmacario@gmail.com>

# Environment variables to be used for customizing built image
#
ENV TINC_HOSTNAME=mygmcont22
ENV TINC_IPADDRESS=10.23.3.22
#
# FIXME: Make sure you fetch rsa_key.priv from
# https://raw.githubusercontent.com/SOLARMA/hostconfig/master/ninuxto/tincgm01/etc/tinc/ninuxto/rsa_key.priv
#
# RUN mkdir -p /etc/tinc/ninuxto/
# COPY rsa_key.priv /etc/tinc/ninuxto/

USER root

RUN mkdir -p /dev/net && \
    mknod /dev/net/tun c 10 200 && \
    chmod 600 /dev/net/tun
RUN apt-get update -qq && \
    apt-get install -qqy curl git net-tools rsync tinc vim
RUN git clone https://github.com/gmacario/tinc-ninuxto.git
RUN mkdir -p /etc/tinc/ninuxto && \
    rsync -av tinc-ninuxto/hosts/ /etc/tinc/ninuxto/hosts/

# Create /etc/tinc/ninuxto/tinc.conf
RUN cp tinc-ninuxto/sample-tinc.conf /etc/tinc/ninuxto/tinc.conf
RUN sed -i "s/^Name.*$/Name = ${TINC_HOSTNAME}/" /etc/tinc/ninuxto/tinc.conf

# Create /etc/tinc/ninuxto/rsa_key.priv
# RUN curl -o /etc/tinc/ninuxto/rsa_key.priv ${TINC_PRIVATEKEY}
# RUN chmod 600 /etc/tinc/ninuxto/rsa_key.priv

# Create /etc/tinc/ninuxto/tinc-up
RUN cp tinc-ninuxto/sample-tinc-up /etc/tinc/ninuxto/tinc-up
RUN sed -i "s/^ifconfig.*$/ifconfig \$INTERFACE ${TINC_IPADDRESS} netmask 255.255.0.0/" /etc/tinc/ninuxto/tinc-up
RUN chmod 755 /etc/tinc/ninuxto/tinc-up

# Create /etc/tinc/ninuxto/tinc-down
RUN cp tinc-ninuxto/sample-tinc-down /etc/tinc/ninuxto/tinc-down
# RUN sed -i "s/^ifconfig.*$/ifconfig \$INTERFACE down/" /etc/tinc/ninuxto/tinc-down
RUN chmod 755 /etc/tinc/ninuxto/tinc-down

# TEST:
#
# docker-compose build --pull
# docker build --build-arg TINC_PRIVATEKEY=xxx -t xxx mytinc/
# winpty docker run -ti testtinc_tinc
# [ ! -e /dev/net/tun ] && mkdir -p /dev/net && mknod /dev/net/tun c 10 200 && chmod 600 /dev/net/tun
# [ ! -e /etc/tinc/ninuxto/rsa_key.priv ] && curl -o /etc/tinc/ninuxto/rsa_key.priv ${TINC_KEYPRIV_URL} && chmod 600 /etc/tinc/ninuxto/rsa_key.priv
# tincd -n ninuxto --no-detach -d7

# EOF
