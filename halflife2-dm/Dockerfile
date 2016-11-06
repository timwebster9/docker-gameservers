FROM ubuntu

RUN dpkg --add-architecture i386 && \
    apt-get -y update && \
    apt-get -y install mailutils postfix curl wget file gzip bzip2 bsdmainutils unzip p7zip-full unrar-free \
                       python util-linux tmux lib32gcc1 libstdc++6 libstdc++6:i386 libssl1.0.0:i386 && \
    adduser hl2dmserver --gecos "First Last,RoomNumber,WorkPhone,HomePhone" --disabled-password && \
    echo "hl2dmserver:hl2dmserver" | chpasswd

USER hl2dmserver
WORKDIR /home/hl2dmserver

# installer
RUN wget https://gameservermanagers.com/dl/hl2dmserver && \
    chmod +x hl2dmserver && \
    ./hl2dmserver auto-install

# maps
WORKDIR /home/hl2dmserver/downloads
RUN MAP_DIR=/home/hl2dmserver/serverfiles/hl2mp/maps && \
    wget http://files.gamebanana.com/maps/dm_egypt_story_b2.7z && \
    wget http://files.gamebanana.com/maps/dm_basebunker.zip && \
    wget http://files.gamebanana.com/maps/extract_me__nightmare_church_rc4_hd.rar && \
    wget http://files.gamebanana.com/maps/dm_alcys_big_temple.zip && \
    wget http://files.gamebanana.com/maps/dm_diorama_night_v2.zip && \
    wget http://files.gamebanana.com/maps/dm_alcys_factory.zip && \
    wget http://files.gamebanana.com/maps/dm_arctic_vendetta_v3.zip && \
    wget http://files.gamebanana.com/maps/fast_download_ready_.rar && \
    7za e -o$MAP_DIR dm_egypt_story_b2.7z && \
    unzip dm_basebunker.zip -d $MAP_DIR && \
    unrar e extract_me__nightmare_church_rc4_hd.rar && \
    7za e -o$MAP_DIR dm_ob_nightmare_church_rc4.bsp.bz2 && \
    unzip dm_alcys_big_temple.zip -d $MAP_DIR && \
    unzip dm_diorama_night_v2.zip -d $MAP_DIR && \
    unzip dm_alcys_factory.zip -d $MAP_DIR && \
    unzip dm_arctic_vendetta_v3.zip -d $MAP_DIR && \
    unrar e fast_download_ready_.rar && \
    7za e -o$MAP_DIR dm_ob_killbox_gravity_gun.bsp.bz2 && \
    rm -rf *

WORKDIR /home/hl2dmserver

COPY hl2dm-server.cfg /home/hl2dmserver/serverfiles/hl2mp/cfg/
COPY wrapper.sh .

USER root
RUN chown -R hl2dmserver:hl2dmserver /home/hl2dmserver

USER hl2dmserver

ENTRYPOINT ["/bin/bash"]
CMD ["wrapper.sh"]
