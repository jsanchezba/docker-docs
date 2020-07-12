## Docker compose


```
version: '3.7'
services:
  main:
    image: portainer/portainer
    command: -H tcp://tasks.agent:9001 --tlsskipverify
    ports:
      - "9000:9000"
    volumes:
      - data:/data
    networks:
      - agent
    deploy:
      mode: replicated
      replicas: 1
  agent:
    image: portainer/agent
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
      - /var/lib/docker/volumes:/var/lib/docker/volumes
    networks:
      - agent
    deploy:
      mode: global
networks:
  agent:
    driver: overlay
    attachable: true
volumes:
  data:
```