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

I look for the location of the `node_exporter.service` file;

```
(base) [root@hpc01 /]# find . -name node_exporter.service
./sys/fs/cgroup/devices/system.slice/node_exporter.service
./sys/fs/cgroup/pids/system.slice/node_exporter.service
./sys/fs/cgroup/blkio/system.slice/node_exporter.service
./sys/fs/cgroup/memory/system.slice/node_exporter.service
./sys/fs/cgroup/cpu, cpuacct/system.slice/node_exporter.service
./sys/fs/cgroup/systemd/system.slice/node_exporter.service
./etc/systemd/system/multi-user.target.wants/node_exporter.service
./etc/systemd/system/default.target.wants/node_exporter.service
./usr/lib/systemd/system/node_exporter.service
```

Aand I had to do some reconfigurations;

## 1. I checked the current Node Exporter version that was running;

```
(base) [root@hpc01 node_exporter]# node_exporter --version
node_exporter, version 1.3.1 (branch: HEAD, revision: a2321e7b940ddcff26873612bccdf7cd4c42b6b6)
  build user:       root@243aafa5525c
  build date:       20211205-11:09:49
  go version:       go1.17.3
  platform:         linux/amd64

```

## 2. I found the previous `node_exporter` version executable file in `/usr/local/bin` ;

```
(base) [root@hpc01 opt]# cd /usr/local/bin/
(base) [root@hpc01 bin]# ls
2to3-3.7          gcov-dump         gdalwarp       prometheus          stag-findsubtree.pl      x86_64-pc-linux-gnu-g++
alertmanager      gcov-tool         Genesis        promtail            stag-flatten.pl          x86_64-pc-linux-gnu-gcc
amtool            gdaladdo          Genesis.jar    promtool            stag-grep.pl             x86_64-pc-linux-gnu-gcc-7.3.0
aws               gdalbuildvrt      gnmanalyse     prove               stag-handle.pl           x86_64-pc-linux-gnu-gcc-9.2.0
aws_completer     gdal-config       gnmmanage      pydoc3.7            stag-itext2simple.pl     x86_64-pc-linux-gnu-gcc-ar
c++               gdal_contour      idle3.7        python3.7           stag-itext2sxpr.pl       x86_64-pc-linux-gnu-gcc-nm
ccmake            gdaldem           loki           python3.7m          stag-itext2xml.pl        x86_64-pc-linux-gnu-gcc-ranlib
cmake             gdalenhance       nearblack      python3.7m-config   stag-join.pl             xml_grep
cpack             gdal_grid         newrelic       pyvenv-3.7          stag-merge.pl            xml_merge
cpp               gdalinfo          node_exporter  R                   stag-mogrify.pl          xml_pp
...
```

## 3. I removed the previous Node Exporter logical link first;

```
(base) [root@hpc01 bin]# rm node_exporter 
rm: remove regular file ‘node_exporter’? yes

```

## 4. I then created the logical link to the current node_exporter version;

```
(base) [root@hpc01 bin]# cd /home/cyndiekamau/logs/prometheus/node_exporter/
(base) [root@hpc01 node_exporter]# ln -s node_exporter-1.5.0.linux-amd64/ /usr/local/bin/node_exporter

```
The logical link allows us to create systemd unit file without needing to update it each time we upgrade node_exporter.

## 5. I then found 2 `node_exporter.service` files already configured, in `/etc/systemd/system` directory;

In `multi-user.target.wants ` and `default.target.wants` directories;

```
(base) [root@hpc01 system]# cd multi-user.target.wants/
(base) [root@hpc01 multi-user.target.wants]# ls
abrt-ccpp.service          ipmievd.service         nginx.service           slurmctld.service
abrtd.service              ipmi.service            node_exporter.service   slurmdbd.service
....
```

```
(base) [root@hpc01 system]# cd default.target.wants/
(base) [root@hpc01 default.target.wants]# ls
node_exporter.service  systemd-readahead-collect.service  systemd-readahead-replay.service

```

Here's the content of the `node_exporter.service` files;

```
[Unit]
Description=Node Exporter
After=network.target

[Service]
Type=simple
User=prometheus
Group=prometheus
ExecStart=/usr/local/bin/node_exporter/node_exporter

[Install]
WantedBy=multi-user.target

```

## 6. I reloaded the systemd daemon;

```
(base) [root@hpc01 multi-user.target.wants]# systemctl daemon-reload
(base) [root@hpc01 multi-user.target.wants]# 
```

## 7. I then restarted the Node Explorer daemon;

```
(base) [root@hpc01 multi-user.target.wants]# systemctl restart node_exporter
(base) [root@hpc01 multi-user.target.wants]# systemctl status node_exporter
● node_exporter.service - Node Exporter
   Loaded: loaded (/usr/lib/systemd/system/node_exporter.service; enabled; vendor preset: disabled)
   Active: active (running) since Mon 2023-01-30 10:55:33 EAT; 12s ago
 Main PID: 52343 (node_exporter)
    Tasks: 6
   Memory: 3.6M
   CGroup: /system.slice/node_exporter.service
           └─52343 /usr/local/bin/node_exporter/node_exporter

Jan 30 10:55:33 hpc01.icipe.org node_exporter[52343]: ts=2023-01-30T07:55:33.376Z caller=node_exporter.go:117 level=info colle...l_zone
Jan 30 10:55:33 hpc01.icipe.org node_exporter[52343]: ts=2023-01-30T07:55:33.376Z caller=node_exporter.go:117 level=info collector=time
Jan 30 10:55:33 hpc01.icipe.org node_exporter[52343]: ts=2023-01-30T07:55:33.376Z caller=node_exporter.go:117 level=info colle...=timex
Jan 30 10:55:33 hpc01.icipe.org node_exporter[52343]: ts=2023-01-30T07:55:33.376Z caller=node_exporter.go:117 level=info colle...queues
Jan 30 10:55:33 hpc01.icipe.org node_exporter[52343]: ts=2023-01-30T07:55:33.376Z caller=node_exporter.go:117 level=info colle...=uname
Jan 30 10:55:33 hpc01.icipe.org node_exporter[52343]: ts=2023-01-30T07:55:33.376Z caller=node_exporter.go:117 level=info colle...vmstat
Jan 30 10:55:33 hpc01.icipe.org node_exporter[52343]: ts=2023-01-30T07:55:33.377Z caller=node_exporter.go:117 level=info collector=xfs
Jan 30 10:55:33 hpc01.icipe.org node_exporter[52343]: ts=2023-01-30T07:55:33.377Z caller=node_exporter.go:117 level=info collector=zfs
Jan 30 10:55:33 hpc01.icipe.org node_exporter[52343]: ts=2023-01-30T07:55:33.377Z caller=tls_config.go:232 level=info msg="Lis...]:9100
Jan 30 10:55:33 hpc01.icipe.org node_exporter[52343]: ts=2023-01-30T07:55:33.377Z caller=tls_config.go:235 level=info msg="TLS...]:9100

```

## 8. I checked if it was listening on port 9100;

```
(base) [root@hpc01 multi-user.target.wants]# journalctl -eu node_exporter | grep Listening
Jan 30 10:55:33 hpc01.icipe.org node_exporter[52343]: ts=2023-01-30T07:55:33.377Z caller=tls_config.go:232 level=info msg="Listening on" address=[::]:9100

```
## 9. I tested by doing a manual scraping on port 9100;

```
(base) [root@hpc01 multi-user.target.wants]# curl localhost:9100/metrics
# HELP go_gc_duration_seconds A summary of the pause duration of garbage collection cycles.
# TYPE go_gc_duration_seconds summary
go_gc_duration_seconds{quantile="0"} 0
go_gc_duration_seconds{quantile="0.25"} 0
go_gc_duration_seconds{quantile="0.5"} 0
go_gc_duration_seconds{quantile="0.75"} 0
go_gc_duration_seconds{quantile="1"} 0
go_gc_duration_seconds_sum 0
go_gc_duration_seconds_count 0
# HELP go_goroutines Number of goroutines that currently exist.
# TYPE go_goroutines gauge
go_goroutines 7
# HELP go_info Information about the Go environment.
# TYPE go_info gauge
go_info{version="go1.19.3"} 1
# HELP go_memstats_alloc_bytes Number of bytes allocated and still in use.
# TYPE go_memstats_alloc_bytes gauge
go_memstats_alloc_bytes 1.440536e+06
# HELP go_memstats_alloc_bytes_total Total number of bytes allocated, even if freed.
# TYPE go_memstats_alloc_bytes_total counter
....
# TYPE node_cooling_device_cur_state gauge
node_cooling_device_cur_state{name="0",type="Processor"} 0
node_cooling_device_cur_state{name="1",type="Processor"} 0
node_cooling_device_cur_state{name="10",type="Processor"} 0
node_cooling_device_cur_state{name="11",type="Processor"} 0
node_cooling_device_cur_state{name="12",type="Processor"} 0
node_cooling_device_cur_state{name="13",type="Processor"} 0
node_cooling_device_cur_state{name="14",type="Processor"} 0
node_cooling_device_cur_state{name="15",type="Processor"} 0
node_cooling_device_cur_state{name="16",type="Processor"} 0
node_cooling_device_cur_state{name="17",type="Processor"} 0
.....
# TYPE node_cooling_device_max_state gauge
node_cooling_device_max_state{name="0",type="Processor"} 10
node_cooling_device_max_state{name="1",type="Processor"} 3
node_cooling_device_max_state{name="10",type="Processor"} 3
node_cooling_device_max_state{name="11",type="Processor"} 3
node_cooling_device_max_state{name="12",type="Processor"} 3
node_cooling_device_max_state{name="13",type="Processor"} 3
node_cooling_device_max_state{name="14",type="Processor"} 3
node_cooling_device_max_state{name="15",type="Processor"} 3
.....
# HELP node_cpu_frequency_max_hertz Maximum cpu thread frequency in hertz.
# TYPE node_cpu_frequency_max_hertz gauge
node_cpu_frequency_max_hertz{cpu="0"} 2.3e+09
node_cpu_frequency_max_hertz{cpu="1"} 2.3e+09
node_cpu_frequency_max_hertz{cpu="10"} 2.3e+09
node_cpu_frequency_max_hertz{cpu="11"} 2.3e+09
node_cpu_frequency_max_hertz{cpu="12"} 2.3e+09
node_cpu_frequency_max_hertz{cpu="13"} 2.3e+09
node_cpu_frequency_max_hertz{cpu="14"} 2.3e+09
node_cpu_frequency_max_hertz{cpu="15"} 2.3e+09
node_cpu_frequency_max_hertz{cpu="16"} 2.3e+09
node_cpu_frequency_max_hertz{cpu="17"} 2.3e+09
node_cpu_frequency_max_hertz{cpu="18"} 2.3e+09
...
# HELP node_filesystem_files Filesystem total file nodes.
# TYPE node_filesystem_files gauge
node_filesystem_files{device="/dev/mapper/centos-home",fstype="xfs",mountpoint="/home"} 2.09717248e+08
node_filesystem_files{device="/dev/mapper/centos-root",fstype="xfs",mountpoint="/"} 2.62144e+08
node_filesystem_files{device="/dev/mapper/centos-tmp",fstype="xfs",mountpoint="/tmp"} 2.097152e+08
node_filesystem_files{device="/dev/mapper/centos-var",fstype="xfs",mountpoint="/var"} 4.194304e+08
node_filesystem_files{device="/dev/mapper/hpc1-scratch",fstype="ext4",mountpoint="/scratch"} 9.8304e+07
node_filesystem_files{device="/dev/mapper/hpc2-apps",fstype="ext4",mountpoint="/opt"} 2.34881024e+08
node_filesystem_files{device="/dev/mapper/hpc2-data",fstype="ext4",mountpoint="/data"} 1.14089984e+08
.....
```

## 10. I now configured Prometheus manual scraping;

As we want to be able to scrape many hosts, we’ll put the list of targets to scrape in a separate file to make it easier to manage.

### First I created a new directory called `targets.d` in `/etc/prometheus`;

```
(base) [root@hpc01 /]# mkdir /etc/prometheus/targets.d
```

### I then created a new file called `node.yml` with the following contents;

```
(base) [root@hpc01 targets.d]# cat node.yml 
- targets:
    - 'hpc01.icipe.org:9100'
(base) [root@hpc01 targets.d]# 

```
### I then edited the `prometheus.yml` file under `/home/cyndiekamau/logs/prometheus/prometheus-2.41.0.linux-amd64` directory, where I downloaded prometheus;

```
global:
  scrape_interval: 10s

scrape_configs:
  - job_name: 'prometheus_master'
    scrape_interval: 5s
    static_configs:
    - targets: ['hpc01.icipe.org:9100']

    # metrics_path defaults to '/metrics'
    # scheme defaults to 'http'.

    metrics_path: '/prometheus/metrics'

  - job_name: 'node_exporter'
    static_configs:
    - targets: ['hpc01.icipe.org:9100']
    - targets: ['10.0.0.215:9100']
  - job_name: "node"
    file_sd_configs:
    - files:
       - /etc/prometheus/targets.d/node.yml
      labels:
       resin_app: RESIN_APP_ID
       resin_device_uuid: RESIN_DEVICE_UUID

alerting:
  alertmanagers:
  - static_configs:
    - targets:
      - localhost:9093
rule_files:
  - 'alerts/rules.yml'


```

### I then cross checked the YAML file for errors using Prometheus' `promtool`;

```
(base) [root@hpc01 prometheus-2.41.0.linux-amd64]# /home/cyndiekamau/logs/prometheus/prometheus-2.41.0.linux-amd64/promtool check config /home/cyndiekamau/logs/prometheus/prometheus-2.41.0.linux-amd64/prometheus.yml 
Checking /home/cyndiekamau/logs/prometheus/prometheus-2.41.0.linux-amd64/prometheus.yml
  FAILED: parsing YAML file /home/cyndiekamau/logs/prometheus/prometheus-2.41.0.linux-amd64/prometheus.yml: yaml: unmarshal errors:
  line 23: field labels not found in type file.plain

```

### So line 23 on `labels` is not allowed, I removed it. I cross checked again;

```
(base) [root@hpc01 prometheus-2.41.0.linux-amd64]# /home/cyndiekamau/logs/prometheus/prometheus-2.41.0.linux-amd64/promtool check config /home/cyndiekamau/logs/prometheus/prometheus-2.41.0.linux-amd64/prometheus.yml 
Checking /home/cyndiekamau/logs/prometheus/prometheus-2.41.0.linux-amd64/prometheus.yml
  FAILED: "/home/cyndiekamau/logs/prometheus/prometheus-2.41.0.linux-amd64/alerts/rules.yml" does not point to an existing file

```
### So I had not given out the absolute path for the `rule_files`. Here's the final draft for the yml file;

```
(base) [root@hpc01 prometheus-2.41.0.linux-amd64]# cat prometheus.yml 
global:
  scrape_interval: 10s

scrape_configs:
  - job_name: 'prometheus_master'
    scrape_interval: 5s
    static_configs:
    - targets: ['hpc01.icipe.org:9100']

    # metrics_path defaults to '/metrics'
    # scheme defaults to 'http'.

    metrics_path: '/prometheus/metrics'

  - job_name: 'node_exporter'
    static_configs:
    - targets: ['hpc01.icipe.org:9100']
    - targets: ['10.0.0.215:9100']
  - job_name: "node"
    file_sd_configs:
    - files:
       - /etc/prometheus/targets.d/node.yml
   
alerting:
  alertmanagers:
  - static_configs:
    - targets:
      - localhost:9093
rule_files:
  - /etc/prometheus/alerts/rules.yml

```

### Crosschecking using the promtool;

```
(base) [root@hpc01 prometheus-2.41.0.linux-amd64]# /home/cyndiekamau/logs/prometheus/prometheus-2.41.0.linux-amd64/promtool check config /home/cyndiekamau/logs/prometheus/prometheus-2.41.0.linux-amd64/prometheus.yml 
Checking /home/cyndiekamau/logs/prometheus/prometheus-2.41.0.linux-amd64/prometheus.yml
  SUCCESS: 1 rule files found
 SUCCESS: /home/cyndiekamau/logs/prometheus/prometheus-2.41.0.linux-amd64/prometheus.yml is valid prometheus config file syntax

Checking /etc/prometheus/alerts/rules.yml
  SUCCESS: 32 rules found

```
It's a success.

## 11. I started the Prometheus server as a background process;

```
(base) [root@hpc01 prometheus-2.41.0.linux-amd64]# nohup ./prometheus > prometheus.log 2>&1 &
[1] 10808

```

## 12. I then checked the logs on the `prometheus` directory  to confirm everything's alright;

```
(base) [root@hpc01 prometheus-2.41.0.linux-amd64]# tail prometheus.log 
ts=2023-01-31T08:22:47.660Z caller=head.go:612 level=info component=tsdb msg="Replaying WAL, this may take a while"
ts=2023-01-31T08:22:47.664Z caller=head.go:683 level=info component=tsdb msg="WAL segment loaded" segment=0 maxSegment=0
ts=2023-01-31T08:22:47.664Z caller=head.go:720 level=info component=tsdb msg="WAL replay completed" checkpoint_replay_duration=949.947µs wal_replay_duration=3.467896ms wbl_replay_duration=325ns total_replay_duration=4.484381ms
ts=2023-01-31T08:22:47.670Z caller=main.go:1014 level=info fs_type=XFS_SUPER_MAGIC
ts=2023-01-31T08:22:47.670Z caller=main.go:1017 level=info msg="TSDB started"
ts=2023-01-31T08:22:47.670Z caller=main.go:1197 level=info msg="Loading configuration file" filename=prometheus.yml
ts=2023-01-31T08:22:47.733Z caller=main.go:1234 level=info msg="Completed loading of configuration file" filename=prometheus.yml totalDuration=62.404592ms db_storage=11.557µs remote_storage=11.346µs web_handler=2.904µs query_engine=1.912µs scrape=749.385µs scrape_sd=143.877µs notify=266.747µs notify_sd=169.311µs rules=59.839395ms tracing=71.779µs
ts=2023-01-31T08:22:47.733Z caller=main.go:978 level=info msg="Server is ready to receive web requests."
ts=2023-01-31T08:22:47.733Z caller=manager.go:953 level=info component="rule manager" msg="Starting rule manager..."
ts=2023-01-31T08:23:10.545Z caller=notifier.go:532 level=error component=notifier alertmanager=http://localhost:9093/api/v2/alerts count=2 msg="Error sending alert" err="Post \"http://localhost:9093/api/v2/alerts\": dial tcp [::1]:9093: connect: connection refused"

```
### You can see the error message `Error sending alert` indicates that Prometheus was unable to send alerts to Alertmanager. The reason is that the connection to http://localhost:9093/api/v2/alerts was refused.

### Let's first check if Alertmanager is running;

```
(base) [root@hpc01 prometheus-2.41.0.linux-amd64]# systemctl status alertmanager
● alertmanager.service - Alert Manager
   Loaded: loaded (/usr/lib/systemd/system/alertmanager.service; enabled; vendor preset: disabled)
   Active: failed (Result: start-limit) since Thu 2022-11-10 13:54:19 EAT; 2 months 21 days ago
 Main PID: 3440 (code=exited, status=1/FAILURE)

Warning: Journal has been rotated since unit was started. Log output is incomplete or unavailable.

```

### Yep so Alertmanager was not running. Let's restart it;

```
(base) [root@hpc01 prometheus-2.41.0.linux-amd64]# systemctl status alertmanager
● alertmanager.service - Alert Manager
   Loaded: loaded (/usr/lib/systemd/system/alertmanager.service; enabled; vendor preset: disabled)
   Active: active (running) since Tue 2023-01-31 11:25:29 EAT; 3s ago
 Main PID: 13993 (alertmanager)
    Tasks: 20
   Memory: 34.6M
   CGroup: /system.slice/alertmanager.service
           └─13993 /usr/local/bin/alertmanager --config.file=/etc/alertmanager/alertmanager.yml --storage.path=/data/alertmanager

Jan 31 11:25:29 hpc01.icipe.org alertmanager[13993]: level=info ts=2023-01-31T08:25:29.643Z caller=main.go:225 msg="Starting A...7d54)"
Jan 31 11:25:29 hpc01.icipe.org alertmanager[13993]: level=info ts=2023-01-31T08:25:29.643Z caller=main.go:226 build_context="...8:55)"
Jan 31 11:25:29 hpc01.icipe.org alertmanager[13993]: level=info ts=2023-01-31T08:25:29.649Z caller=cluster.go:184 component=cl...t=9094
Jan 31 11:25:29 hpc01.icipe.org alertmanager[13993]: level=info ts=2023-01-31T08:25:29.681Z caller=cluster.go:671 component=cl...val=2s
Jan 31 11:25:29 hpc01.icipe.org alertmanager[13993]: level=info ts=2023-01-31T08:25:29.780Z caller=coordinator.go:113 componen...er.yml
Jan 31 11:25:29 hpc01.icipe.org alertmanager[13993]: level=info ts=2023-01-31T08:25:29.804Z caller=coordinator.go:126 componen...er.yml
Jan 31 11:25:29 hpc01.icipe.org alertmanager[13993]: level=info ts=2023-01-31T08:25:29.813Z caller=main.go:518 msg=Listening a...=:9093
Jan 31 11:25:29 hpc01.icipe.org alertmanager[13993]: level=info ts=2023-01-31T08:25:29.813Z caller=tls_config.go:191 msg="TLS ...=false
Jan 31 11:25:31 hpc01.icipe.org alertmanager[13993]: level=info ts=2023-01-31T08:25:31.683Z caller=cluster.go:696 component=cl...36983s
Hint: Some lines were ellipsized, use -l to show in full.

```
