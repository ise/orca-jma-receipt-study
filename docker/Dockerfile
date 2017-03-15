FROM ubuntu:16.04
MAINTAINER ise

ENV USER=ormaster
ENV PASSWORD=ormaster

WORKDIR /tmp
RUN apt-get update
RUN apt-get install -y wget 
RUN wget -q https://ftp.orca.med.or.jp/pub/ubuntu/archive.key
RUN apt-key add archive.key
RUN wget -q -O /etc/apt/sources.list.d/jma-receipt-xenial50.list https://ftp.orca.med.or.jp/pub/ubuntu/jma-receipt-xenial50.list
RUN apt-get update
RUN apt-get dist-upgrade -y
RUN apt-get install -y jma-receipt
RUN apt-get install -y sudo
RUN service postgresql restart && jma-setup && service jma-receipt start && echo 'ormaster:$1$2RaqLgfs$U5Yxojvs7r59aLj2LvNUs1:' > /etc/jma-receipt/passwd && sudo -u orca /usr/lib/jma-receipt/bin/passwd_store.sh

EXPOSE 8000
CMD service postgresql restart && service jma-receipt restart && tail -f /dev/null
