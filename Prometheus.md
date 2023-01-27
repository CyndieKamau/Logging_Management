# Configuration and use of Prometheus Logging tool


# **STEP ONE:INSTALLING PROMETHEUS SERVER**

## 1. Create a directory to store all files for easier management

```
(base) [root@hpc01 cyndiekamau]# mkdir logs
(base) [root@hpc01 cyndiekamau]# cd logs/

```

## 2. Download latest build of prometheus server from github:

```
(base) [root@hpc01 logs]# wget https://github.com/prometheus/prometheus/releases/download/v2.41.0/prometheus-2.41.0.linux-amd64.tar.gz
--2023-01-27 13:28:54--  https://github.com/prometheus/prometheus/releases/download/v2.41.0/prometheus-2.41.0.linux-amd64.tar.gz
Resolving github.com (github.com)... 140.82.121.4
Connecting to github.com (github.com)|140.82.121.4|:443... connected.
HTTP request sent, awaiting response... 302 Found
Location: https://objects.githubusercontent.com/github-production-release-asset-2e65be/6838921/77a09aa5-7a19-4fe8-88fd-1ebeaf3d6130?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAIWNJYAX4CSVEH53A%2F20230127%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20230127T102709Z&X-Amz-Expires=300&X-Amz-Signature=bdb08186ea7ded96a5214b007a18883a58081f19ec539abadd28a479fbcf18e2&X-Amz-SignedHeaders=host&actor_id=0&key_id=0&repo_id=6838921&response-content-disposition=attachment%3B%20filename%3Dprometheus-2.41.0.linux-amd64.tar.gz&response-content-type=application%2Foctet-stream [following]
--2023-01-27 13:28:55--  https://objects.githubusercontent.com/github-production-release-asset-2e65be/6838921/77a09aa5-7a19-4fe8-88fd-1ebeaf3d6130?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAIWNJYAX4CSVEH53A%2F20230127%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20230127T102709Z&X-Amz-Expires=300&X-Amz-Signature=bdb08186ea7ded96a5214b007a18883a58081f19ec539abadd28a479fbcf18e2&X-Amz-SignedHeaders=host&actor_id=0&key_id=0&repo_id=6838921&response-content-disposition=attachment%3B%20filename%3Dprometheus-2.41.0.linux-amd64.tar.gz&response-content-type=application%2Foctet-stream
Resolving objects.githubusercontent.com (objects.githubusercontent.com)... 185.199.111.133, 185.199.108.133, 185.199.109.133, ...
Connecting to objects.githubusercontent.com (objects.githubusercontent.com)|185.199.111.133|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 90331753 (86M) [application/octet-stream]
Saving to: ‘prometheus-2.41.0.linux-amd64.tar.gz’

100%[=============================================================================================>] 90,331,753  8.37MB/s   in 10s    

2023-01-27 13:29:07 (8.35 MB/s) - ‘prometheus-2.41.0.linux-amd64.tar.gz’ saved [90331753/90331753]


```

## 3. Create a parent directory to store all Prometheus components

```
(base) [root@hpc01 logs]# mkdir prometheus
(base) [root@hpc01 logs]# cd prometheus/
(base) [root@hpc01 prometheus]# 

```

## 4. Use `tar` to extract prometheus found in the previously created `logs` directory;

```
(base) [root@hpc01 prometheus]# tar -xvzf ../prometheus-2.41.0.linux-amd64.tar.gz
prometheus-2.41.0.linux-amd64/
prometheus-2.41.0.linux-amd64/consoles/
prometheus-2.41.0.linux-amd64/consoles/node-disk.html
prometheus-2.41.0.linux-amd64/consoles/node-cpu.html
prometheus-2.41.0.linux-amd64/consoles/index.html.example
prometheus-2.41.0.linux-amd64/consoles/node-overview.html
prometheus-2.41.0.linux-amd64/consoles/node.html
prometheus-2.41.0.linux-amd64/consoles/prometheus.html
prometheus-2.41.0.linux-amd64/consoles/prometheus-overview.html
prometheus-2.41.0.linux-amd64/console_libraries/
prometheus-2.41.0.linux-amd64/console_libraries/prom.lib
prometheus-2.41.0.linux-amd64/console_libraries/menu.lib
prometheus-2.41.0.linux-amd64/NOTICE
prometheus-2.41.0.linux-amd64/prometheus
prometheus-2.41.0.linux-amd64/LICENSE
prometheus-2.41.0.linux-amd64/prometheus.yml
prometheus-2.41.0.linux-amd64/promtool
(base) [root@hpc01 prometheus]# 

```

## 5. Verify Installation by checking the Prometheus version;

```
(base) [root@hpc01 prometheus]# ls
prometheus-2.41.0.linux-amd64
(base) [root@hpc01 prometheus]# cd prometheus-2.41.0.linux-amd64/
(base) [root@hpc01 prometheus-2.41.0.linux-amd64]# ./prometheus --version
prometheus, version 2.41.0 (branch: HEAD, revision: c0d8a56c69014279464c0e15d8bfb0e153af0dab)
  build user:       root@d20a03e77067
  build date:       20221220-10:40:45
  go version:       go1.19.4
  platform:         linux/amd64

```

# **STEP TWO:INSTALLING NODE EXPORTER**

## 1. Download Node EXporter's latest build from github, in the `logs` directory:

```
(base) [root@hpc01 prometheus-2.41.0.linux-amd64]# cd ../../
(base) [root@hpc01 logs]# wget https://github.com/prometheus/node_exporter/releases/download/v1.5.0/node_exporter-1.5.0.linux-amd64.tar.gz
--2023-01-27 13:59:42--  https://github.com/prometheus/node_exporter/releases/download/v1.5.0/node_exporter-1.5.0.linux-amd64.tar.gz
Resolving github.com (github.com)... 140.82.121.3
Connecting to github.com (github.com)|140.82.121.3|:443... connected.
HTTP request sent, awaiting response... 302 Found
Location: https://objects.githubusercontent.com/github-production-release-asset-2e65be/9524057/fc1630e0-8913-427f-94ba-4131d3ed96c7?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAIWNJYAX4CSVEH53A%2F20230127%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20230127T105908Z&X-Amz-Expires=300&X-Amz-Signature=489062222fde07c56967195cb7e84cb799cc7cbc8ea4850e9ac914e4e866d99e&X-Amz-SignedHeaders=host&actor_id=0&key_id=0&repo_id=9524057&response-content-disposition=attachment%3B%20filename%3Dnode_exporter-1.5.0.linux-amd64.tar.gz&response-content-type=application%2Foctet-stream [following]
--2023-01-27 13:59:43--  https://objects.githubusercontent.com/github-production-release-asset-2e65be/9524057/fc1630e0-8913-427f-94ba-4131d3ed96c7?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAIWNJYAX4CSVEH53A%2F20230127%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20230127T105908Z&X-Amz-Expires=300&X-Amz-Signature=489062222fde07c56967195cb7e84cb799cc7cbc8ea4850e9ac914e4e866d99e&X-Amz-SignedHeaders=host&actor_id=0&key_id=0&repo_id=9524057&response-content-disposition=attachment%3B%20filename%3Dnode_exporter-1.5.0.linux-amd64.tar.gz&response-content-type=application%2Foctet-stream
Resolving objects.githubusercontent.com (objects.githubusercontent.com)... 185.199.108.133, 185.199.109.133, 185.199.110.133, ...
Connecting to objects.githubusercontent.com (objects.githubusercontent.com)|185.199.108.133|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 10181045 (9.7M) [application/octet-stream]
Saving to: ‘node_exporter-1.5.0.linux-amd64.tar.gz’

100%[=============================================================================================>] 10,181,045  2.80MB/s   in 3.5s   

2023-01-27 13:59:47 (2.80 MB/s) - ‘node_exporter-1.5.0.linux-amd64.tar.gz’ saved [10181045/10181045]

(base) [root@hpc01 logs]# 


```

## 2. Create a new directory called `node_exporter` inside the `prometheus` directory, and get inside it:

```
(base) [root@hpc01 logs]# cd prometheus/
(base) [root@hpc01 prometheus]# mkdir node_exporter && cd ./node_exporter
(base) [root@hpc01 node_exporter]# 

```

## 3. Use `tar` command to extract Node Exporter in the `logs` directory;

```
(base) [root@hpc01 node_exporter]# tar -xvzf ../../node_exporter-1.5.0.linux-amd64.tar.gz
node_exporter-1.5.0.linux-amd64/
node_exporter-1.5.0.linux-amd64/LICENSE
node_exporter-1.5.0.linux-amd64/NOTICE
node_exporter-1.5.0.linux-amd64/node_exporter
(base) [root@hpc01 node_exporter]# 

```

# **STEP THREE: RUNNING NODE EXPORTER AS A SERVICE**

## 1. Use `nano` or `vi` to create a unit configuration file called `node_exporter.service`.

```
(base) [root@hpc01 node_exporter]# nano /etc/systemd/system/node_exporter.service
```

## 2. Add the following to the configuration file;

*  Path of the `node_exporter` executable
*  Which user should run the executable

```
(base) [root@hpc01 system]# cat node_exporter.service
[Unit]
Description=Node Exporter

[Service]
User=prometheus
ExecStart=/home/prometheus/prometheus/node_exporter/node_exporter

[Install]
WantedBy=default.target
(base) [root@hpc01 system]# 

```

## 3. Reload `systemd` to read the configuration file;

```
(base) [root@hpc01 system]# systemctl daemon-reload
```

## 4. Enable it so that it starts automatically at boot time.

```
(base) [root@hpc01 system]# systemctl enable node_exporter.service
Failed to execute operation: File exists

```

In my case, I got the systemctl error; I checked whether `node_exporter.service` was already enabled;

```
(base) [root@hpc01 system]# systemctl is-enabled 'node_exporter.service'
enabled

```

Yeep already enabled. Weird huh!!

Checking using `systemctl`;

```
(base) [root@hpc01 system]# systemctl status node_exporter.service
● node_exporter.service - Node Exporter
   Loaded: loaded (/etc/systemd/system/node_exporter.service; enabled; vendor preset: disabled)
   Active: active (running) since Thu 2022-11-10 13:54:16 EAT; 2 months 17 days ago
 Main PID: 3123 (node_exporter)
   CGroup: /system.slice/node_exporter.service
           └─3123 /usr/local/bin/node_exporter

Jan 27 14:16:37 hpc01.icipe.org systemd[1]: Current command vanished from the unit file, execution of the command list won't ...esumed.
Jan 27 14:17:43 hpc01.icipe.org systemd[1]: [/etc/systemd/system/node_exporter.service:6] Executable path is not absolute, ig...xporter
Jan 27 14:17:43 hpc01.icipe.org systemd[1]: node_exporter.service lacks both ExecStart= and ExecStop= setting. Refusing.
Warning: Journal has been rotated since unit was started. Log output is incomplete or unavailable.
Hint: Some lines were ellipsized, use -l to show in full.

```
I'll have to remove that config file.
