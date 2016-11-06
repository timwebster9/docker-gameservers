FROM ubuntu

RUN dpkg --add-architecture i386 && \
    apt-get -y update && \
    apt-get -y install mailutils postfix curl wget file gzip bzip2 bsdmainutils unzip \
                       python util-linux tmux lib32gcc1 libstdc++6 libstdc++6:i386 libssl1.0.0:i386 && \
    adduser svenserver --gecos "First Last,RoomNumber,WorkPhone,HomePhone" --disabled-password && \
    echo "svenserver:svenserver" | chpasswd

USER svenserver
WORKDIR /home/svenserver

RUN wget https://gameservermanagers.com/dl/svenserver && \
    chmod +x svenserver && \
    ./svenserver auto-install && \
    wget http://scmapdb.com/local--files/mappack:classic-map-pack/svencoop_classic.zip && \
    wget http://servers.snarkcafe.net/scmapdb/40_mappack.zip && \
    wget http://scmapdb.com/local--files/mappack:creepsworld-map-pack/sc4_creepsworld_v3.zip && \
    unzip svencoop_classic.zip -d /home/svenserver/serverfiles/svencoop && \
    unzip -o 40_mappack.zip -d /home/svenserver/serverfiles/svencoop && \
    unzip -o sc4_creepsworld_v3.zip -d /home/svenserver/serverfiles/svencoop && \
    rm svencoop_classic.zip 40_mappack.zip sc4_creepsworld_v3.zip

COPY server.cfg /home/svenserver/serverfiles/svencoop/
COPY svenwrapper.sh .

USER root
RUN chown -R svenserver:svenserver /home/svenserver/serverfiles/svencoop/server.cfg

USER svenserver

ENTRYPOINT ["/bin/bash"]
CMD ["svenwrapper.sh"]
