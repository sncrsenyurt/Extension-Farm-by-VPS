
# extension-farm

## We start by installing Docker on our virtual server.

```
sudo apt update -y && sudo apt upgrade -y
for pkg in docker.io docker-doc docker-compose podman-docker containerd runc; do sudo apt-get remove $pkg; done

sudo apt-get update
sudo apt-get install ca-certificates curl gnupg
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg

echo \
  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt update -y && sudo apt upgrade -y

sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

# Docker version check
docker --version
```

## After installing Docker, we check the server's time zone, which is important.

```
realpath --relative-to /usr/share/zoneinfo /etc/localtime
```

## Chromium Installation

**First, we prepare space on the server for Chromium**

```
mkdir chromium
cd chromium
```

**Create the Docker compose file**

```
nano docker-compose.yaml
```

```
---
services:
  chromium:
    image: lscr.io/linuxserver/chromium:latest
    container_name: chromium
    security_opt:
      - seccomp:unconfined #optional
    environment:
      - CUSTOM_USER=     #Replace username
      - PASSWORD=    #Replace password
      - PUID=1000
      - PGID=1000
      - TZ=Europe/London
      - CHROME_CLI=https://github.com/hitasyurekk #optional
    volumes:
      - /root/chromium/config:/config
    ports:
      - 3010:3000   #Change 3010 to your favorite port if needed
      - 3011:3001   #Change 3011 to your favorite port if needed
    shm_size: "1gb"
    restart: unless-stopped
```

<code> Ctrl+X+Y+Enter </code> **Use these commands to save and exit the file.**

## Final step: Running Chromium

```
cd $HOME && cd chromium

docker compose up -d
```

## You are now ready. The next step is to connect to the server from your computer and install the extensions.

```
http://Server_IP:3010/
https://Server_IP:3011/
```

# Step 2: Install the extensions!

**I recommend creating a new account on these servers. You can use your existing account if you prefer, but it’s safer to create a new one.**

Nodepay: [https://app.nodepay.ai/register?ref=OcK6UeIDXtTJaBN](https://app.nodepay.ai/register?ref=9m0tkzTTQxoq7y2)

UpNetwork: https://points.upnetwork.xyz/?request=122473

Gradient: https://app.gradient.network/signup?code=OKZ66P

Block mesh: https://app.blockmesh.xyz/register?invite_code=rove

Teneo: https://teneo.pro/community-node **Access code: GRRqs**
