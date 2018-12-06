# DOCKER NGROK IMAGE

## BUILD IMAGE

```linux
git clone https://github.com/happyshi0402/docker-ngrok1.git docker-ngrok
cd docker-ngrok
docker build -t happyshi0402/ngrok .
```

## RUN
* you must mount your folder (E.g `/data/ngrok`) to container `/myfiles`
* if it is the first run, it will generate the binaries file and CA in your floder `/data/ngrok`

```linux
docker run -idt --name ngrok-server \
-v /data/ngrok:/myfiles \
-e DOMAIN='tunnel.hteen.cn' happyshi0402/ngrok /bin/sh /server.sh
```
