# Welcome to SubQuery Network in Linux!
<img width="700" alt="Screen Shot 2022-11-01 at 20 54 41" src="https://blog.subquery.network/content/images/size/w1200/2024/02/subquery-network-coming.png">

## Recommended hardware requirements
- CPU: 16 CPU
- Memory: 32 GB RAM
- Disk: 4 TB SSD Storage
>Storage requirements will vary based on various factors (age of the chain, transaction rate, etc)

## Official documentation:

- How to Become an Indexer [here](https://academy.subquery.network/subquery_network/node_operators/setup/becoming-a-node-operator.html)

- Install Indexing Service on Linux [here](https://academy.subquery.network/subquery_network/node_operators/setup/install-linux.html#step-4-start-node-operator-services)


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
curl https://raw.githubusercontent.com/subquery/network-indexer-services/main/deploy/docker-compose.yml -o docker-compose.yml

# extra steps to use local ipfs node
mkdir ipfs
curl https://raw.githubusercontent.com/subquery/network-indexer-services/main/deploy/ipfs/ipfs.sh -o ipfs/ipfs.sh
chmod +x ipfs/ipfs.sh
```
This will overwrite the existing docker-compose.yml file.

Make sure the indexer service versions are correct:


| Service                        | Version   |
| :----------------------------- | :-------- |
| onfinality/subql-coordinator   | v2.0.7    |
| onfinality/subql-indexer-proxy | v2.1.0    |

>Important
>
>Please go through the docker-compose file carefully, and change the following parameters to your own values:
>- POSTGRES_PASSWORD
>- postgres-password
>- secret-key
>- jwt-secret

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

## 5. SSL Certificate Configuration

### Why should you configure and enable a SSL certificate?

SSL certificate is an important way to secure your indexer service and encrypt traffic between your query service and the Consumers requesting data from it. It's a good idea to obtain an SSL certificate for any professional service and SubQuery is no different. Additionally, a SSL certificate is required for when a Consumer access a website via SSL and that website is requesting data from your SubQuery project.

**Since it's such a standard best practice, although it's not required, wee rank Indexer higher in the Indexer leaderboard if they have SSL enabled.**

### How do I know that an Indexer has SSL enabled

The `Proxy Server Endpoint` in indexer's metadata will start with `https` instead of `http`.

### Enabling SSL

### 5.1. Purchase a domain name

You can purchase a domain from a lot of domain providers, we won't be providing a guide on how to do this. The rest of this guide assumes you have purchased `mysqindexer.com`

### 5.2. Config DNS

Add a A record to your domain that points to your indexer's server IP address. For example, we add an A record for `proxy.mysqindexer.com` to our server's IP `210.10.5.61`.

### 5.3. Get a SSL Cert

You can get a free SSL Cert from [Let's Encrypt](https://letsencrypt.org/), they offer a lot of ways to get a SSL Cert, you can choose the [one that fits your needs](https://letsencrypt.org/docs/client-options/).

This tutorial will use Certbot + NGINX + Ubuntu as an example.

#### 5.3.1 Install Certbot

Check [https://certbot.eff.org/instructions](https://certbot.eff.org/instructions) on how to do this step

#### 5.3.2 Install & Config NGINX
##### 5.3.2.1 Install Nginx
We will use nginx for two purpose. 
1. Listen on port 1080 to allow Let's encrypt to verify your domain name.
2. As a reverse proxy to forward traffic from port 443 (https) to indexer-proxy.
```shell
sudo apt install -y nginx
```

##### 5.3.2.2 Reconfig indexer-proxy
In the default settings, indexer-proxy listen on port 80, now we need to change it to 1080. 
```shell
# docker-compose.yml
proxy:
    image: subquerynetwork/indexer-proxy:v2.1.0
    container_name: indexer_proxy
    restart: always
    ports:
      - 1080:1080
    command:
      - --port=1080
      - --auth
      - --network=mainnet # network type, need to be same with coordinator
      - --jwt-secret=<a random str> # change to any random string value
      - --secret-key=<a random str> # keep same with coordinator secret key
      - --coordinator-endpoint=http://indexer_coordinator:8000
      - --network-endpoint=https://mainnet.base.org # network endpoint, can choose your own endpoint
      - --token-duration=24 # query auth token validity [hours]
      - --redis-endpoint=redis://indexer_cache
      - --metrics-token=thisismyAuthtoken # change to any random string value
```
then restart the indexer-proxy container
```shell
docker-compose up -d --no-deps proxy
```
##### 5.3.2.3 Config NGINX
Edit your NGINX configuration to add the following (e.g. it would usually be at `/etc/nginx/sites-available/proxy.mysqindexer.com`)

```shell
# /etc/nginx/sites-available/proxy.mysqindexer.com
server {
    listen 443 ssl http2; // Update the ports to listen on
    listen [::]:443 ssl http2;

    server_name proxy.mysqindexer.com; // update the server name to match your DNS address

    location / {
      proxy_pass      http://127.0.0.1:1080;
    }

}

# link the new configution with a symlink to your edited file
sudo ln -s /etc/nginx/sites-available/proxy.mysqindexer.com /etc/nginx/sites-enabled/proxy.mysqindexer.com
```

Then finish configuration.
##### 5.3.2.3 Run certbot
```bash
# run certbot
sudo certbot --nginx -d proxy.mysqindexer.com

# output
# Saving debug log to /var/log/letsencrypt/letsencrypt.log
# Requesting a certificate for proxy.mysqindexer.com

# Successfully received certificate.
# Certificate is saved at: /etc/letsencrypt/live/proxy.mysqindexer.com/fullchain.pem
# Key is saved at:         /etc/letsencrypt/live/proxy.mysqindexer.com/privkey.pem
# This certificate expires on 2023-08-06.
# These files will be updated when the certificate renews.
# Certbot has set up a scheduled task to automatically renew this certificate in the background.
#
# Deploying certificate
# Successfully deployed certificate for proxy.mysqindexer.com to /etc/nginx/sites-enabled/proxy.mysqindexer.com
# Congratulations! You have successfully enabled HTTPS on https://proxy.mysqindexer.com
#
# - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
# If you like Certbot, please consider supporting our work by:
#  * Donating to ISRG / Let's Encrypt:   https://letsencrypt.org/donate
#  * Donating to EFF:                    https://eff.org/donate-le
# - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
```

### 5.4. Update your indexer metadata

Update your indexer metadata, set the `Proxy Server Endpoint` to `https://proxy.mysqindexer.com`


## ALL DONE!!!
