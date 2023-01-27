# Configuration and use of Prometheus Logging tool


# **STEP ONE:**

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


