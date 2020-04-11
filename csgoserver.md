
===== SERVER CS GO IPTABLE ==========
iptables -A INPUT -i eth0 -p tcp --dport 27015 -j ACCEPT
iptables -A INPUT -i eth0 -p udp --dport 27015 -j ACCEPT
iptables -A INPUT -i eth0 -p tcp --dport 27020 -j ACCEPT
iptables -A INPUT -i eth0 -p udp --dport 27020 -j ACCEPT


docker run \
  --rm \
  --interactive \
  --tty \
  --detach \
  --mount source=csgo-data,target=/home/steam/csgo \
  --publish 27015:27015/tcp \
  --publish 27015:27015/udp \
  --publish 27020:27020/tcp \
  --publish 27020:27020/udp \
  --env "SERVER_HOSTNAME=hostname" \
  --env "SERVER_PASSWORD=password" \
  --env "RCON_PASSWORD=rconpassword" \
  --env "STEAM_ACCOUNT=gamelogintoken" \
  --env "AUTHKEY=webapikey" \
  --env "SOURCEMOD_ADMINS=STEAM_1:0:123456,STEAM_1:0:654321" \
  kmallea/csgo
