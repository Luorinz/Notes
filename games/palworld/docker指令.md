docker run -d \
    --name palworld-server \
    -p 8211:8211/udp \
    -p 27015:27015/udp \
    -v ~/servers/palworld-server:/palworld/ \
    -e PUID=1000 \
    -e PGID=1000 \
    -e PORT=8211 \
    -e PLAYERS=4 \
    -e MULTITHREADING=true \
    -e RCON_ENABLED=true \
    -e RCON_PORT=25575 \
    -e TZ=Asia/Shanghai \
    -e ADMIN_PASSWORD=123456 \
    -e SERVER_PASSWORD=123456 \
    -e COMMUNITY=false \
    -e SERVER_NAME=Anda \
    -e AUTO_PAUSE_ENABLED=true \
    -e PAL_EGG_DEFAULT_HATCHING_TIME=0 \
    -e DEATH_PENALTY=ItemAndEquipment \
    -e ENABLE_NON_LOGIN_PENALTY=false \
    --restart unless-stopped \
    --stop-timeout 30 \
    thijsvanloef/palworld-server-docker:latest



