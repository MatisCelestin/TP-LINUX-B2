# TP2 : Utilisation courante de Docker

## I. Commun à tous : App Web

### 🌞 docker-compose.yml

[docker-compose.yml](./docker-compose.yml)

# TP2 dév : packaging et environnement de dév local

## 1. Calculatrice

### 🌞 Le lien vers ton dépôt

[calculatrice](https://github.com/MatisCelestin/calculatrice-linux)

## 2. Chat room

### 🌞 Packager l'application de chat room

[chat_room](https://github.com/MatisCelestin/chat-room-linux)

## 3. Ur own

### 🌞 Packager une application à vous
Application réaliser avec Dany en B1
[hangman_web](https://github.com/danyGhassan/hangman_web)

# TP2 admins : Web stack

## I. Good practices

### 🌞 Limiter l'accès aux ressources
```
matis@ThinkPad:~/projets/TP-LINUX-B2$ docker run --memory=1g --cpus=1 -it test1 bash
root@eg9417445ae:/#  
```

### 🌞 No root

```
matis@ThinkPad:~/poubelle$ cat Dockerfile 
FROM nginx:latest
RUN useradd -ms /bin/bash testUser
USER testUser
WORKDIR /home/testUser
```

### 🌞 Mode read-only

```
docker run -d -p 80:80 --read-only -v $(pwd)/nginx-cache:/var/cache/nginx -v $(pwd)/nginx-pid:/var/run testu_ser_nginx
55d26d172973efac9417ef29085b8395d5da30dff38649b5b88086a679b5d3e0
```
## II. Reverse proxy buddy

## A. Simple HTTP setup

### 🌞 Adaptez le docker-compose.yml de la partie précédente

[docker compose](./docker-compose.yml)

```
matis@ThinkPad:~$ curl www.supersite.com
[{"id":"bob","name":1},{"id":"martin","name":2},{"id":"pikachu","name":3},{"id":"shibboleth","name":4}]
matis@ThinkPad:~$ curl www.supersite.com | grep tropdecode
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   104  100   104    0     0  33429      0 --:--:-- --:--:-- --:--:-- 34666
```

## B. HTTPS auto-signé

### 🌞 HTTPS auto-signé# TP2 : Utilisation courante de Docker

[http-auto](./Dossier-conf/https-auto)
