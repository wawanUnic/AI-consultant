# Automation service n8n

### Web panel - port 5678

Working not from root

Launching the container. We will work without encryption, because the primary physical balancer (HaProxy) is responsible for encryption. The configuration is performed for the domain name nero-n8n.duckdns.org
```
sudo docker run -d --restart unless-stopped -it \
--name n8n \
--add-host host.docker.internal:host-gateway \
-p 5678:5678 \ 
-e N8N_HOST="nero-n8n.duckdns.org" \
-e WEBHOOK_TUNNEL_URL="https://nero-n8n.duckdns.org/" \
-e WEBHOOK_URL="https://nero-n8n.duckdns.org/" \
-e N8N_SECURE_COOKIE="false" \
-v n8n_data:/home/node/.n8n \
n8nio/n8n
```

Debugging
```
sudo docker ps -a
```

Update
```
Сделать резервную копию /var/lib/docker/volumes/n8n_data
sudo docker stop n8n
sudo docker rm n8n
sudo docker images
sudo docker rmi [имя образа n8n]
docker pull n8nio/n8n
[заново запустить контейнер командой, описанной выше]
```
