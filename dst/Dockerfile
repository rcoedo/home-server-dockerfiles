# Thanks to dst-academy/server

FROM ubuntu:14.04

ENV CONF_DIR="DoNotStarveTogether" \
	DEFAULT_SERVER_NAME="Dont Starve Together" \
	DEFAULT_SERVER_DESCRIPTION="" \
	SERVER_PORT=10999 \
	OFFLINE_SERVER=false \
	MAX_PLAYERS=4 \
	WHITELIST_SLOTS=0 \
	PVP=false \
	GAME_MODE=survival \
	SERVER_INTENTION=cooperative \
	ENABLE_AUTOSAVER=true \
	TICK_RATE=15 \
	CONNECTION_TIMEOUT=5000 \
	ENABLE_VOTE_KICK=true \
	PAUSE_WHEN_EMPTY=true \
	STEAM_APP_ID=343050 \
	STEAM_AUTHENTICATION_PORT=8766 \
	STEAM_MASTER_SERVER_PORT=27016 \
	STEAM_GROUP_ONLY=false \
	STEAM_GROUP_ADMINS=false \
	CONSOLE_ENABLED=true \
	AUTOCOMPILER_ENABLED=true \
	MODS_ENABLED=true \
	SHARD_ENABLE=false \
	IS_MASTER=false \
	BIND_IP="0.0.0.0" \
	DISABLECLOUD=true

RUN dpkg --add-architecture i386 \
	&& apt-get update -y \
	&& apt-get install -y curl lib32gcc1 lib32stdc++6 libcurl4-gnutls-dev:i386 \
	&& apt-get clean \
	&& rm -rf /var/lib/apt/lists/*

RUN useradd -m steam

COPY ./scripts/entrypoint.sh /home/steam/
RUN chmod +x /home/steam/entrypoint.sh

USER steam

RUN cd /home/steam \
	&& curl -SLO "http://media.steampowered.com/installer/steamcmd_linux.tar.gz" \
	&& tar -xvf steamcmd_linux.tar.gz -C /home/steam \
	&& rm steamcmd_linux.tar.gz

RUN /home/steam/steamcmd.sh \
	+@ShutdownOnFailedCommand 1 \
	+@NoPromptForPassword 1 \
	+login anonymous \
	+force_install_dir /home/steam/DoNotStarveTogether \
	+app_update ${STEAM_APP_ID} validate \
	+quit

EXPOSE 10999/udp

WORKDIR /home/steam/DoNotStarveTogether/data/
ENTRYPOINT ["/home/steam/entrypoint.sh"]
