FROM ubuntu:latest
MAINTAINER Tiago Gasiba "tiago.gasiba@gmail.com"

RUN apt-get update
RUN apt install -y openvpn iptables bash && \
    rm -rf /tmp/* /var/tmp/* /var/cache/apk/* /var/cache/distfiles/*

# cp /tmp/{server.crt,ca.crt} /etc/openvpn/
COPY EasyRSA-3.0.4/pki/issued/server.crt  /etc/openvpn/server.crt
COPY EasyRSA-3.0.4/pki/ca.crt             /etc/openvpn/ca.crt
# sudo cp ~/EasyRSA-3.0.4/ta.key /etc/openvpn/
COPY EasyRSA-3.0.4/ta.key                 /etc/openvpn/ta.key
# sudo cp ~/EasyRSA-3.0.4/pki/dh.pem /etc/openvpn/
COPY EasyRSA-3.0.4/pki/dh.pem             /etc/openvpn/dh.pem

RUN sed -i '/net.ipv4.ip_forward/d' /etc/sysctl.conf
RUN echo "net.ipv4.ip_forward=1" >> /etc/sysctl.conf

EXPOSE 1194/udp

#RUN apt-get install -y python python-pip wget
#RUN pip install Flask
#
#ADD hello.py /home/hello.py
#
#WORKDIR /home
