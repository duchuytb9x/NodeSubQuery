# Welcome to Kepler!
<img width="700" alt="Screen Shot 2022-11-01 at 20 54 41" src="https://blog.subquery.network/content/images/size/w1200/2023/04/kepler-on-poly.png">

## Recommended hardware requirements
- CPU: 2 CPU
- Memory: 8 GB RAM
- Disk: 400 GB SSD Storage
>Storage requirements will vary based on various factors (age of the chain, transaction rate, etc)

## Official documentation:

- How to Become an Indexer [here](https://academy.subquery.network/subquery_network/kepler/indexers/become-an-indexer.html)

- Install Indexing Service on Linux [here](https://academy.subquery.network/subquery_network/kepler/indexers/install-indexer-linux.html)


## 1. Install Docker and Docker-Compose:
- Get update:
```
sudo apt-get update
```

- Install the docker:
```
sudo apt install docker.io
```

- Install the docker-compose:
```
# get the latest version for docker-compose
sudo curl -L https://github.com/docker/compose/releases/latest/download/docker-compose-$(uname -s)-$(uname -m) -o /usr/bin/docker-compose

# fix permissions after download:
sudo chmod +x /usr/bin/docker-compose

# verify the installation
sudo docker-compose version

```
## 2. Download the Docker Compose File for Indexer Services:
Run the following command:
```
mkdir subquery-indexer && cd subquery-indexer
curl https://raw.githubusercontent.com/subquery/indexer-services/kepler/docker-compose.yml -o docker-compose.yml
```

>Important
>
>Please change the **POSTGRES_PASSWORD** in postgres and **postgres-password** in coordinator-service to your own one

## 3. Start Indexer Services:

Run the service using the following command::
```
sudo docker-compose up -d
```

It will start the following services:

- coordinator_db
- coordinator_service
- coordinator_proxy
- proxy-redis

## 4. Set Up Auto Start:

Create `/etc/systemd/system/subquery.service.` 

Run the service using the following command::
```
sudo nano /etc/systemd/system/subquery.service
```

Coppy and Paste:

```
[Unit]
Description="Subquery systemd service"
After=network.target
StartLimitIntervalSec=0

[Service]
Type=simple
Restart=on-failure
RestartSec=10
User=root
SyslogIdentifier=subquery
SyslogFacility=local7
KillSignal=SIGHUP
WorkingDirectory=/root/subquery-indexer
ExecStart=/usr/bin/docker-compose up -d

[Install]
WantedBy=multi-user.target
```

Register and start the service by running:
```
systemctl enable subquery.service
systemctl start subquery.service
```

After that, verify that the service is running:
```
systemctl status subquery.service
```

## Do you need a server?
- Use the links with referal programm <a href="https://www.vultr.com/?ref=8997131"><img width="200" src="https://user-images.githubusercontent.com/90826754/200262610-b6251a9b-36a9-44f7-be30-fa691e7238de.png" a>
            <a href="https://www.digitalocean.com/?refcode=87b8b298c106&utm_campaign=Referral_Invite&utm_medium=Referral_Program&utm_source=badge"><img src="https://web-platforms.sfo2.cdn.digitaloceanspaces.com/WWW/Badge%201.svg" alt="DigitalOcean Referral Badge" /></a>

**NOTE!: use a referal link & you will get 100$ to your server provider account**

ALL DONE!!!
