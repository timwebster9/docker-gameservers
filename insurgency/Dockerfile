FROM ubuntu:17.04

RUN dpkg --add-architecture i386 \
  && apt-get update \
  && apt-get -y install mailutils binutils \
    postfix curl wget file bzip2 gzip unzip \
    bsdmainutils python util-linux ca-certificates \
    tmux lib32gcc1 libstdc++6 libstdc++6:i386 locales

RUN locale-gen en_GB.UTF-8 \
    && update-locale LANG=en_GB.UTF-8 \
    && adduser insserver --gecos "First Last,RoomNumber,WorkPhone,HomePhone" --disabled-password \
	  && echo "insserver:insserver" | chpasswd \
    && usermod -G tty insserver

ENV LANG "en_GB.UTF-8"
ENV LC_ALL "en_GB.UTF-8"
ENV LANGUAGE "en_GB.UTF-8"

COPY serverlist.csv /home/insserver/lgsm/tmp/data/
COPY linuxgsm.sh /home/insserver/

RUN chown -R insserver:insserver /home/insserver

USER insserver
WORKDIR /home/insserver

RUN bash linuxgsm.sh insserver\
  && ./insserver auto-install

COPY wrapper.sh /home/insserver/

USER root
COPY insserver.cfg /home/insserver/serverfiles/insurgency/cfg/
RUN chown -R insserver:insserver /home/insserver/serverfiles/insurgency/cfg/insserver.cfg

USER insserver

ENTRYPOINT ["/bin/bash"]
CMD ["wrapper.sh"]