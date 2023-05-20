<h1 align="center"> System monitoring with Grafana, Prometheus, Node Exporter </h1>

<img width="1275" alt="Screenshot_6" src="https://github.com/duchuytb9x/NodeSubQueryKepler/assets/32235812/12263fc0-de19-45db-a22f-7facbd1bbc24">

# I. Install Grafana
**`Step 1: Update system`**

```sh
sudo apt update
```
**`Step 2: Add Grafana APT repository`**

- Add Grafana gpg key which allows you to install signed packages.
```sh
sudo apt install -y gnupg2 curl software-properties-common
curl -fsSL https://packages.grafana.com/gpg.key|sudo gpg --dearmor -o /etc/apt/trusted.gpg.d/grafana.gpg
```
- Then install Grafana APT repository:
```sh
sudo add-apt-repository "deb https://packages.grafana.com/oss/deb stable main"
```
**`Step 3: Install Grafana`**
- Install Grafana
```sh
sudo apt update
sudo apt -y install grafana
```
- Start Grafana Service.
```sh
sudo systemctl enable --now grafana-server
```
- Check Grafana Status
```
systemctl status grafana-server.service
```
- The result will be as follows
```
* grafana-server.service - Grafana instance
     Loaded: loaded (/lib/systemd/system/grafana-server.service; enabled; vendor preset: enabled)
     Active: active (running) since Fri 2022-12-02 09:38:37 +07; 4 days ago
       Docs: http://docs.grafana.org
   Main PID: 343342 (grafana-server)
      Tasks: 17 (limit: 4616)
     Memory: 78.2M
     CGroup: /system.slice/grafana-server.service
             `-343342 /usr/sbin/grafana-server --config=/etc/grafana/grafana.ini --pidfile=/run/grafana/grafana-server.pid --packaging=deb cfg:default.path>

Dec 06 14:28:41 Prometheus-Obj grafana-server[343342]: logger=cleanup t=2022-12-06T14:28:41.715802349+07:00 level=info msg="Completed cleanup jobs" duratio>
D
```
**`Step 4: Open port fiwall`**
```sh
sudo apt -y install ufw
sudo ufw enable
sudo ufw allow 3000/tcp
```
# II. Install Prometheus
# 1. Setup Prometheus
**`Step 1: Add User Prometheus`**
```sh
sudo useradd --no-create-home --shell /bin/false prometheus
```
**`Step 2: Create data & configs folder for Prometheus`**
```sh
sudo mkdir -p /var/lib/prometheus
sudo mkdir -p /etc/prometheus/
```

**`Step 3: Download Prometheus`**
- Install wget.
```sh
sudo apt update
sudo apt -y install wget curl vim
```
- Download latest binary archive for Prometheus.
```sh
mkdir -p /tmp/prometheus && cd /tmp/prometheus
curl -s https://api.github.com/repos/prometheus/prometheus/releases/latest | grep browser_download_url | grep linux-amd64 | cut -d '"' -f 4 | wget -qi -
```
- Extract the file:
```sh
tar xvf prometheus*.tar.gz
cd prometheus*/
```
- Move the binary files to `/usr/local/bin/` directory.
```sh
sudo mv prometheus promtool /usr/local/bin/
```
- Check version
```sh
promtool --version
prometheus --version
```
- Move the system configuration file to `/etc`
```sh
sudo mv prometheus.yml /etc/prometheus/prometheus.yml
```
- Also move consoles and console_libraries to /etc/prometheus directory:
```sh
sudo mv consoles/ console_libraries/ /etc/prometheus/
cd $HOME
```
**`Step 4: Configure Prometheus`**
- Create or edit a configuration file for Prometheus `/etc/prometheus/prometheus.yml`
```sh
sudo vi /etc/prometheus/prometheus.yml
```
  - The template
  ```sh
global:
  scrape_interval: 10s

scrape_configs:
  - job_name: 'prometheus'
    scrape_interval: 5s
    static_configs:
      - targets: ['localhost:9090']
```
- Create a file to manage the service system
```sh
sudo tee /etc/systemd/system/prometheus.service<<EOF
[Unit]
Description=Prometheus
Documentation=https://prometheus.io/docs/introduction/overview/
Wants=network-online.target
After=network-online.target

[Service]
Type=simple
Environment="GOMAXPROCS=1"
User=prometheus
Group=prometheus
ExecReload=/bin/kill -HUP $MAINPID
ExecStart=/usr/local/bin/prometheus \
  --config.file=/etc/prometheus/prometheus.yml \
  --storage.tsdb.path=/var/lib/prometheus \
  --web.console.templates=/etc/prometheus/consoles \
  --web.console.libraries=/etc/prometheus/console_libraries \
  --web.listen-address=0.0.0.0:9090 \
  --storage.tsdb.retention.time=90d \
  --web.enable-admin-api

SyslogIdentifier=prometheus
Restart=always

[Install]
WantedBy=multi-user.target
EOF
```
- Change folder permissions
```sh
sudo chown prometheus:prometheus /etc/prometheus
sudo chown prometheus:prometheus /var/lib/prometheus
sudo chown prometheus:prometheus /usr/local/bin/prometheus
sudo chown prometheus:prometheus /usr/local/bin/promtool
sudo chown -R prometheus:prometheus /etc/prometheus/consoles
sudo chown -R prometheus:prometheus /etc/prometheus/console_libraries
```
- Reload systemd daemon and start the service
```sh
sudo systemctl daemon-reload
sudo systemctl start prometheus
sudo systemctl enable prometheus
```

- Check status using systemctl status prometheus
```sh
systemctl status prometheus
```
 - The result will be as follows:
 ```
root@PhanDucHuy:~# 
● prometheus.service - Prometheus
     Loaded: loaded (/etc/systemd/system/prometheus.service; enabled; vendor preset: enabled)
     Active: active (running) since Thu 2023-05-18 18:03:35 CEST; 1 day 18h ago
       Docs: https://prometheus.io/docs/introduction/overview/
   Main PID: 519154 (prometheus)
      Tasks: 8 (limit: 9457)
     Memory: 47.9M
        CPU: 6min 3.465s
     CGroup: /system.slice/prometheus.service
             └─519154 /usr/local/bin/prometheus --config.file=/etc/prometheus/prometheus.yml --web.config.file=/etc/prometheus/web.yml --storage.tsdb.path=/var/lib/prometheus>

May 20 07:00:07 vmi871283.contaboserver.net prometheus[519154]: ts=2023-05-20T05:00:07.166Z caller=compact.go:464 level=info component=tsdb msg="compact blocks" count=3 mint=>
May 20 07:00:07 vmi871283.contaboserver.net prometheus[519154]: ts=2023-05-20T05:00:07.175Z caller=db.go:1552 level=info component=tsdb msg="Deleting obsolete block" block=01>
May 20 07:00:07 vmi871283.contaboserver.net prometheus[519154]: ts=2023-05-20T05:00:07.191Z caller=db.go:1552 level=info component=tsdb msg="Deleting obsolete block" block=01>
May 20 07:00:07 vmi871283.contaboserver.net prometheus[519154]: ts=2023-05-20T05:00:07.198Z caller=db.go:1552 level=info component=tsdb msg="Deleting obsolete block" block=01>
May 20 09:00:04 vmi871283.contaboserver.net prometheus[519154]: ts=2023-05-20T07:00:04.086Z caller=compact.go:523 level=info component=tsdb msg="write block" mint=16845552016>
May 20 09:00:04 vmi871283.contaboserver.net prometheus[519154]: ts=2023-05-20T07:00:04.216Z caller=head.go:1286 level=info component=tsdb msg="Head GC completed" caller=trunc>
May 20 09:00:04 vmi871283.contaboserver.net prometheus[519154]: ts=2023-05-20T07:00:04.252Z caller=checkpoint.go:100 level=info component=tsdb msg="Creating checkpoint" from_>
May 20 09:00:05 vmi871283.contaboserver.net prometheus[519154]: ts=2023-05-20T07:00:05.899Z caller=head.go:1254 level=info component=tsdb msg="WAL checkpoint complete" first=>
May 20 11:00:03 vmi871283.contaboserver.net prometheus[519154]: ts=2023-05-20T09:00:03.466Z caller=compact.go:523 level=info component=tsdb msg="write block" mint=16845624016>
May 20 11:00:03 vmi871283.contaboserver.net prometheus[519154]: ts=2023-05-20T09:00:03.504Z caller=head.go:1286 level=info component=tsdb msg="Head GC completed" caller=trunc>
```
- Allow Port 9090
```sh
sudo ufw allow 9090/tcp
```

- Check Prometheus Server Access `http://IP:9090`

## 2. Security settings for website password authentication for Prometheus (Optional)
**`Step 1: Hashing a password`**

- Install package requirements
```sh
sudo apt update
sudo apt install python3-bcrypt -y
```
- Once installed, create a python script that will prompt for the password.
```sh
# vi gen-pass.py
import getpass
import bcrypt

password = getpass.getpass("password: ")
hashed_password = bcrypt.hashpw(password.encode("utf-8"), bcrypt.gensalt())
print(hashed_password.decode())
```
- Save and Run Scripts
```sh
python3 gen-pass.py
```
- Password Initialization
```sh
password: 123456
$2b$12$Ru/58U9Hw5nQZRiXkKObYeIC.ZZWpxxPn9O1Xlq9LPCMozG7di8hi
```

**`Step 2: Initialize yaml Web file`**

-  tao file .yaml
```sh
# vi /etc/prometheus/web.yml
basic_auth_users:
       admin: '$2b$12$Ru/58U9Hw5nQZRiXkKObYeIC.ZZWpxxPn9O1Xlq9LPCMozG7di8hi'
```
> Note: replace the content of the encrypted key with the key created in `Step 1`


- Verify configuration file
```sh
# promtool check web-config /etc/prometheus/web.yml
/etc/prometheus/web.yml SUCCESS
```

**`Step 3: Launch Prometheus Server`**

- Update your Prometheus systemd unit file
```sh
# sudo vi /etc/systemd/system/prometheus.service
[Unit]
Description=Prometheus
Documentation=https://prometheus.io/docs/introduction/overview/
Wants=network-online.target
After=network-online.target

[Service]
Type=simple
Environment="GOMAXPROCS=1"
User=prometheus
Group=prometheus
ExecReload=/bin/kill -HUP $MAINPID
ExecStart=/usr/local/bin/prometheus \
  --config.file=/etc/prometheus/prometheus.yml \
  --web.config.file=/etc/prometheus/web.yml \
  --storage.tsdb.path=/var/lib/prometheus \
  --web.console.templates=/etc/prometheus/consoles \
  --web.console.libraries=/etc/prometheus/console_libraries \
  --web.listen-address=0.0.0.0:9090 \
  --storage.tsdb.retention.time=90d \
  --web.enable-admin-api

SyslogIdentifier=prometheus
Restart=always

[Install]
WantedBy=multi-user.target
```

- restart the Prometheus Server
```sh
sudo systemctl daemon-reload
sudo systemctl restart prometheus
sudo systemctl enable prometheus
```

- Confirm Prometheus service is started without errors
```sh
root@PhanDucHuy:~# systemctl status prometheus
* prometheus.service - Prometheus
     Loaded: loaded (/etc/systemd/system/prometheus.service; enabled; vendor preset: enabled)
     Active: active (running) since Mon 2022-12-05 13:43:40 +07; 1 day 1h ago
       Docs: https://prometheus.io/docs/introduction/overview/
   Main PID: 381247 (prometheus)
      Tasks: 13 (limit: 4616)
     Memory: 80.8M
     CGroup: /system.slice/prometheus.service
             `-381247 /usr/local/bin/prometheus --config.file=/etc/prometheus/prometheus.yml --web.config.file=/etc/prometheus/web.yml --storage.tsdb.path=>

Dec 06 12:00:06 Prometheus-Obj prometheus[381247]: ts=2022-12-06T05:00:06.468Z caller=db.go:1541 level=info component=tsdb msg="Deleting obsolete block" bl>
Dec 06 12:00:06 Prometheus-Obj prometheus[381247]: ts=2022-12-06T05:00:06.782Z caller=compact.go:460 level=info component=tsdb msg="compact blocks" count=3>
Dec 06 12:00:06 Prometheus-Obj prometheus[381247]: ts=2022-12-06T05:00:06.790Z caller=db.go:1541 level=info component=tsdb msg="Deleting obsolete block" bl>
D
```

- Check Access Authentication
```sh
$ curl -u admin http://localhost:9090/metrics
Enter host password for user 'admin': <Enter the set password>
```
```sh
$ curl -u admin http://localhost:9090/metrics
Enter host password for user 'admin':
Unauthorized
```

# III. Install Node Exporter
## 1. Setup Node Exporter
**`Step 1: Add User`**
```sh
useradd -rs /bin/false nodeusr
```
**`Step 2: Download Node Exporter`**
- Install wget.
```sh
sudo apt update
sudo apt -y install wget curl vim
```
- Download latest binary archive for Node Exporter.
```sh
curl -s https://api.github.com/repos/prometheus/node_exporter/releases/latest | grep browser_download_url | grep linux-amd64 | cut -d '"' -f 4 | wget -qi -
```
- Extract the file:
```sh
tar xvf node_exporter*.tar.gz
cd node_exporter*/
```
- Move the binary files to /usr/local/bin/ directory.
```sh
sudo mv node_exporter /usr/local/bin/
```
- Check version
```sh
node_exporter --version
```
**`Step 3: Node Exporter`**
- Create or edit a service system file for Node Exporter – `/etc/systemd/system/node_exporter.service`
```sh
sudo tee /etc/systemd/system/node_exporter.service<<EOF
[Unit]
Description=Node Exporter
After=network.target

[Service]
User=nodeusr
Group=nodeusr
Type=simple
ExecStart=/usr/local/bin/node_exporter

[Install]
WantedBy=multi-user.target
EOF
```
- Reload systemd daemon and start the service
```sh
sudo systemctl daemon-reload
sudo systemctl start node_exporter
sudo systemctl enable node_exporter
```

- Check status using systemctl status node_exporter
```sh
root@PhanDucHuy:~# systemctl status node_exporter
● node_exporter.service - Node Exporter
     Loaded: loaded (/etc/systemd/system/node_exporter.service; enabled; vendor preset: enabled)
     Active: active (running) since Thu 2023-05-18 16:29:42 CEST; 1 day 19h ago
   Main PID: 478398 (node_exporter)
      Tasks: 5 (limit: 9457)
     Memory: 14.8M
        CPU: 12min 18.227s
     CGroup: /system.slice/node_exporter.service
             └─478398 /usr/local/bin/node_exporter

Notice: journal has been rotated since unit was started, output may be incomplete.
```
- Allow Port 9100
```sh
sudo ufw allow 9100/tcp
```

- Node Exporter Server Access Test `http://IP:9100`

**`Step 4: Configure Prometheus`**
- Edit a configuration file for Prometheus – `/etc/prometheus/prometheus.yml`
```sh
sudo vi /etc/prometheus/prometheus.yml
```
  - The template
  ```sh
global:
  scrape_interval: 10s

scrape_configs:
  - job_name: 'prometheus'
    scrape_interval: 5s
    static_configs:
      - targets: ['localhost:9090']

  - job_name: 'node_exporter'
    scrape_interval: 5s
    static_configs:
      - targets: ['localhost:9100']
```
- Restart the Prometheus Server
```sh
sudo systemctl daemon-reload
sudo systemctl restart prometheus
```
- Check status of Prometheus
```sh
sudo systemctl status prometheus
```

## 2. Security settings for website password authentication for Node Exporter (Optional)
**`Step 1: Hashing a password`**

- Install package requirements
```sh
apt install apache2-utils
```
- Gen pass
```
htpasswd -nBC 10 "" | tr -d ':\n'; echo
```
- Initialize yaml config file
```sh
# cat /etc/node-exporter/config.yml
basic_auth_users:
  prometheus: <the-output-value-of-htpasswd>
```
**`Step 2: Launch Prometheus Server`**

- Update your Node Exporter systemd unit file
```sh
sudo tee /etc/systemd/system/node_exporter.service<<EOF
[Unit]
Description=Node Exporter
After=network.target

[Service]
User=nodeusr
Group=nodeusr
Type=simple
ExecStart=/usr/local/bin/node_exporter --web.config.file=/etc/node-exporter/config.yml

[Install]
WantedBy=multi-user.target
EOF
```

- Restart the Prometheus Server
```sh
sudo systemctl daemon-reload
sudo systemctl restart prometheus
sudo systemctl enable prometheus
```

- Confirm Prometheus service is started without errors
```sh
systemctl status prometheus
```
- The result will be as follows:
```
● node_exporter.service - Node Exporter
     Loaded: loaded (/etc/systemd/system/node_exporter.service; enabled; vendor preset: enabled)
     Active: active (running) since Thu 2023-05-18 21:51:32 EDT; 1 day 8h ago
   Main PID: 730704 (node_exporter)
      Tasks: 6 (limit: 19119)
     Memory: 10.0M
        CPU: 9min 36.059s
     CGroup: /system.slice/node_exporter.service
             └─730704 /usr/local/bin/node_exporter --web.config.file=/etc/node-exporter/config.yml

May 18 21:51:33 vmi1291386.contaboserver.net node_exporter[730704]: ts=2023-05-19T01:51:33.000Z caller=node_exporter.go:117 level=info collector=thermal_zone
May 18 21:51:33 vmi1291386.contaboserver.net node_exporter[730704]: ts=2023-05-19T01:51:33.000Z caller=node_exporter.go:117 level=info collector=time
May 18 21:51:33 vmi1291386.contaboserver.net node_exporter[730704]: ts=2023-05-19T01:51:33.001Z caller=node_exporter.go:117 level=info collector=timex
May 18 21:51:33 vmi1291386.contaboserver.net node_exporter[730704]: ts=2023-05-19T01:51:33.001Z caller=node_exporter.go:117 level=info collector=udp_queues
May 18 21:51:33 vmi1291386.contaboserver.net node_exporter[730704]: ts=2023-05-19T01:51:33.001Z caller=node_exporter.go:117 level=info collector=uname
May 18 21:51:33 vmi1291386.contaboserver.net node_exporter[730704]: ts=2023-05-19T01:51:33.001Z caller=node_exporter.go:117 level=info collector=vmstat
May 18 21:51:33 vmi1291386.contaboserver.net node_exporter[730704]: ts=2023-05-19T01:51:33.001Z caller=node_exporter.go:117 level=info collector=xfs
May 18 21:51:33 vmi1291386.contaboserver.net node_exporter[730704]: ts=2023-05-19T01:51:33.001Z caller=node_exporter.go:117 level=info collector=zfs
May 18 21:51:33 vmi1291386.contaboserver.net node_exporter[730704]: ts=2023-05-19T01:51:33.001Z caller=tls_config.go:232 level=info msg="Listening on" address=[::]:9100
May 18 21:51:33 vmi1291386.contaboserver.net node_exporter[730704]: ts=2023-05-19T01:51:33.002Z caller=tls_config.go:271 level=info msg="TLS is disabled." http2=false address>
```

- Check Access Authentication
```sh
$ curl -u prometheus http://localhost:9100/metrics
Enter host password for user 'prometheus': <Enter the set password>
```
```sh
$ curl -u prometheus http://localhost:9100/metrics
Enter host password for user 'prometheus':
Unauthorized
```

**`Step 3: Configure Prometheus`**
- Edit a configuration file for Prometheus – `/etc/prometheus/prometheus.yml`
```sh
sudo vi /etc/prometheus/prometheus.yml
```
  - The template
  ```sh
global:
  scrape_interval: 10s

scrape_configs:
  - job_name: 'prometheus'
    scrape_interval: 5s
    static_configs:
      - targets: ['localhost:9090']

  - job_name: 'node_exporter'
    scrape_interval: 5s
    static_configs:
      - targets: ['localhost:9100']
    basic_auth:
      username: prometheus
      password: "123456"
```
- Restart the Prometheus Server
```sh
sudo systemctl daemon-reload
sudo systemctl restart prometheus
```
- Check status of Prometheus
```sh
sudo systemctl status prometheus
```
# Initialize Dashboard
**`Step 1: Log in to Grafana`**

Go to http://IP:3000
<img width="1275" alt="Screenshot_2" src="https://github.com/duchuytb9x/NodeSubQueryKepler/assets/32235812/bf827430-4022-4d35-aca2-55438045e45e">
Login to grafana with username and password admin/admin
You will need to change your password after that

**`Step 2: Add data source`**

To add data source you go to `Home > Administration > Data sources > Add data source`
<img width="1275" alt="Screenshot_14" src="https://github.com/duchuytb9x/NodeSubQueryKepler/assets/32235812/ab74042e-fc52-4b27-a61a-aca85f4a3e0f">

Enter the address `http://localhost:9000/`, username password then Click `Save & Test`
<img width="1275" alt="Screenshot_1" src="https://github.com/duchuytb9x/NodeSubQueryKepler/assets/32235812/2e639598-be17-4f1a-80f0-a88d08b020ea">

**`Step 3: Add Dashboard`**

To add data Dashboard you go to `Home > Dashboards > New > Import`
<img width="1275" alt="Screenshot_3" src="https://github.com/duchuytb9x/NodeSubQueryKepler/assets/32235812/236cf8e7-cfa9-4f68-a220-dc261c30d3b6">

Enter `1860` in the textbox `Import via grafana.com` then Click `Load`
<img width="1275" alt="Screenshot_4" src="https://github.com/duchuytb9x/NodeSubQueryKepler/assets/32235812/cc8d6d30-891a-493e-87f2-774fbc4a1b13">

Select prometheus source then Click `Import`
<img width="1275" alt="Screenshot_5" src="https://github.com/duchuytb9x/NodeSubQueryKepler/assets/32235812/a66c3bbd-7eb3-4a99-a317-d9b7b9dbd0a8">

And here is the result:
<img width="1275" alt="Screenshot_6" src="https://github.com/duchuytb9x/NodeSubQueryKepler/assets/32235812/9ce51c2d-219e-43bb-8565-ed562bcbac81">

ALL DONE!!!
