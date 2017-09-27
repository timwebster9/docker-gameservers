FROM ubuntu:17.04

RUN dpkg --add-architecture i386 \
  && apt-get update \
  && apt-get -y install mailutils binutils postfix curl wget file bzip2 gzip unzip bsdmainutils python util-linux ca-certificates tmux lib32gcc1 libstdc++6 libstdc++6:i386

RUN  adduser insserver --gecos "First Last,RoomNumber,WorkPhone,HomePhone" --disabled-password && \
	echo "insserver:insserver" | chpasswd

COPY serverlist.csv /home/insserver/lgsm/tmp/data/
COPY linuxgsm.sh /home/insserver/

RUN chown -R insserver:insserver /home/insserver

USER insserver
WORKDIR /home/insserver

RUN bash linuxgsm.sh insserver\
  && ./insserver auto-install





