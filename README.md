## This is a notepad for code snippets and random useful commands

```
config.vm.provider "virtualbox" do |v|
  v.memory = 1024
  v.cpus = 2
end
```
```
tail -f -n 50 /var/log/secure | grep sshd
journalctl -e
ss -tunlp4
nc IP -u PORTA #netcat
```

##### docker change default mount point
```
sudo systemctl stop docker
sudo systemctl status docker
ps faux | grep -i docker
mkdir /opt/app #directory where to put the default docker files
rsync -avxP  /var/lib/docker/ /opt/app
sudo nano /lib/systemd/system/docker.service
ExecStart=/usr/bin/dockerd -g /opt/app -H fd:// --containerd=/run/containerd/containerd.sock
sudo systemctl daemon-reload
systemctl start docker
```
```
curl -fsSL https://get.docker.com | bash

url https://releases.rancher.com/install-docker/19.03.sh | sh
 
sudo usermod -aG docker vagrant
 
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"

# KUBERNETES 
kubectl label nodes NOMEDONODE kubernetes.io/role=worker

# EDIT DEPLOYMENT
Kubectl edit deployment/rancher -n cattle-system
```
##### mount a point with exec permission
```
mount /opt/ -o remount,exec
and restart the Docker engine.
```
##### Docker commands to remove all containers and all images
```
#DOCKER IMAGES REMOVE ALL
docker image rm $(docker image ls -a -q)

#DOCKER REMOVE ALL CONTAINERS
docker container rm -f $(docker container ls -a -q)

#get out of container w/o stopping it
CTRL + P + Q

docker commit IDCONTAINER  nome:versão
```
##### DOCKER RUN WITH VOLUMES
```
#RUN MYSQL DOCKER CONTAINER
docker volume create mysql-volume
docker run --name mysql -p3306:3306 -v mysql-volume:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=yourpass -d mysql/mysql:8.0

#RUN GRAFANA DOCKER CONTAINER
docker run -d -p 3000:3000 --name grafana grafana/grafana

#RUN PHPMYADMIN
docker run --name phpmyadmin -v phpmyadmin-volume:/etc/phpmyadmin/config.user.inc.php --link mysql:db -p 82:80 -d phpmyadmin/phpmyadmin

-v mysql_data:/var/lib/mysql
-v glpi_data:/var/www/html/
```
##### PHP CONFIG
```
file_uploads = On
allow_url_fopen = On
short_open_tag = On
memory_limit = 256M
cgi.fix_pathinfo = 0
upload_max_filesize = 100M
max_execution_time = 360
max_input_vars = 1500
date.timezone = America/Sao_Paulo
```
```
chown -R www-data:www-data /var/www/html && chmod -R 755 /var/ww/html
```
##### Reset glpi password to defautl
```
use glpi;
update glpi.glpi_users set password='$2y$10$p..X4No3kbL9zq3s9yyXuuNdbHN78Bd/j8aiInj5L7Fo1Hg3hJMFa' where name = 'glpi';
quit;
```
##### Server config to create a reverse nginx proxy for multime instances
```
server {
    server_name YOURDOMAINHERE;
    server_name_in_redirect off;
    proxy_set_header Host $host:$server_port;

    location / {
      proxy_pass http://127.0.0.1:8002;
    }
}

server {
    listen 80;
    server_name YOURDOMAINHERE;
    server_name_in_redirect off;
    proxy_set_header Host $host:$server_port;

    location / {
      proxy_pass http://127.0.0.1:8080;
    }
}
```
##### Docker registry commando to show images
```
http://ubntsrv:5000/v2/_catalog
```




