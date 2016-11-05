FROM ubuntu

RUN dpkg --add-architecture i386 && \
    apt-get -y update && \
    apt-get -y install mailutils postfix curl wget file gzip bzip2 bsdmainutils \
                       python util-linux tmux lib32gcc1 libstdc++6 libstdc++6:i386 libssl1.0.0:i386 && \
    adduser svenserver --gecos "First Last,RoomNumber,WorkPhone,HomePhone" --disabled-password && \
    echo "svenserver:svenserver" | chpasswd

USER svenserver
WORKDIR /home/svenserver

RUN wget https://gameservermanagers.com/dl/svenserver && \
    chmod +x svenserver && \
    ./svenserver auto-install && \
    wget http://scmapdb.com/local--files/mappack:classic-map-pack/svencoop_classic.zip && \
    unzip svencoop_classic.zip -d /home/svenserver/serverfiles/svencoop && \
    rm svencoop_classic.zip

COPY svenwrapper.sh .

ENTRYPOINT ["/bin/bash"]
CMD ["svenwrapper.sh"]