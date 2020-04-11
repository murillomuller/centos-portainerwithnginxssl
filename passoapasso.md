yum update

yum install iptables-services

systemctl enable iptables

systemctl enable ip6tables

//VISUALIZAR REGRAS IPTABLES
cat /etc/sysconfig/iptables


yum install -y yum-utils

yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo

yum install docker-ce docker-ce-cli containerd.io

systemctl start docker

systemctl enable docker

=========================================================

docker volume create portainer_data

docker run --name portainer -d -p 9000:9000 -v/var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data --env "VIRTUAL_HOST=vps.7virtual.online" --env "VIRTUAL_PORT=9000" --env "LETSENCRYPT_HOST=vps.7virtual.online" portainer/portainer

docker run --detach --name nginx-proxy --publish 80:80 --publish 443:443 --volume /etc/nginx/certs --volume /etc/nginx/vhost.d --volume /usr/share/nginx/html --volume /var/run/docker.sock:/tmp/docker.sock:ro jwilder/nginx-proxy

docker run --detach --name nginx-proxy-letsencrypt --volumes-from nginx-proxy --volume /var/run/docker.sock:/var/run/docker.sock:ro --env "DEFAULT_EMAIL=email@email.com.br" jrcs/letsencrypt-nginx-proxy-companion

==========================================
iptables -L -n -v --line-numbers
iptables -P INPUT DROP
iptables -P FORWARD ACCEPT
iptables -P OUTPUT ACCEPT

iptables -A INPUT -i eth0 -p tcp --dport 22 -j ACCEPT
iptables -A INPUT -i eth0 -p tcp --dport 80 -j ACCEPT
iptables -A INPUT -i eth0 -p tcp --dport 443 -j ACCEPT
iptables -A INPUT -i docker0 -j ACCEPT
iptables -A INPUT -p udp --sport 53 -j ACCEPT
iptables -A INPUT -p tcp --sport 53 -j ACCEPT
iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT

service iptables save
service iptables restart


vi /etc/docker/daemon.json
{
"iptables": false
}



