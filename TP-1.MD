# I. Init

- [I. Init](#i-init)
  - [1. sudo c pa bo](#1-sudo-c-pa-bo)
  - [2. Un premier conteneur en vif](#2-un-premier-conteneur-en-vif)
  - [3. Un deuxième conteneur en vif](#3-un-deuxième-conteneur-en-vif)



## 1. sudo c pa bo

🌞 Ajouter votre utilisateur au groupe docker
```
matis@thinkpad:~$ docker run hello-world

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/

```

## 2. Un premier conteneur en vif

🌞 Lancer un conteneur NGINX

```
matis@thinkpad:~$ docker run -d -p 9999:80 nginx
Unable to find image 'nginx:latest' locally
latest: Pulling from library/nginx
bc0965b23a04: Pull complete 
650ee30bbe5e: Pull complete 
8cc1569e58f5: Pull complete 
362f35df001b: Pull complete 
13e320bf29cd: Pull complete 
7b50399908e1: Pull complete 
57b64962dd94: Pull complete 
Digest: sha256:fb197595ebe76b9c0c14ab68159fd3c08bd067ec62300583543f0ebda353b5be
Status: Downloaded newer image for nginx:latest
ef5a6168f3fe6789a29377baa11cc1b04425a9dfa0c3987ac9836c3c42954116
```

🌞 Visitons

vérifier que le conteneur est actif avec une commande qui liste les conteneurs en cours de fonctionnement
```
matis@thinkpad:~$ docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS          PORTS                                     NAMES
ef5a6168f3fe   nginx     "/docker-entrypoint.…"   45 seconds ago   Up 43 seconds   0.0.0.0:9999->80/tcp, [::]:9999->80/tcp   sad_easley
```
afficher les logs du conteneur
```
matis@thinkpad:~$ docker logs sad_easley
/docker-entrypoint.sh: /docker-entrypoint.d/ is not empty, will attempt to perform configuration
/docker-entrypoint.sh: Looking for shell scripts in /docker-entrypoint.d/
/docker-entrypoint.sh: Launching /docker-entrypoint.d/10-listen-on-ipv6-by-default.sh
10-listen-on-ipv6-by-default.sh: info: Getting the checksum of /etc/nginx/conf.d/default.conf
10-listen-on-ipv6-by-default.sh: info: Enabled listen on IPv6 in /etc/nginx/conf.d/default.conf
/docker-entrypoint.sh: Sourcing /docker-entrypoint.d/15-local-resolvers.envsh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/20-envsubst-on-templates.sh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/30-tune-worker-processes.sh
/docker-entrypoint.sh: Configuration complete; ready for start up
2024/12/11 14:43:20 [notice] 1#1: using the "epoll" event method
2024/12/11 14:43:20 [notice] 1#1: nginx/1.27.3
2024/12/11 14:43:20 [notice] 1#1: built by gcc 12.2.0 (Debian 12.2.0-14) 
2024/12/11 14:43:20 [notice] 1#1: OS: Linux 6.8.0-49-generic
2024/12/11 14:43:20 [notice] 1#1: getrlimit(RLIMIT_NOFILE): 1048576:1048576
2024/12/11 14:43:20 [notice] 1#1: start worker processes
2024/12/11 14:43:20 [notice] 1#1: start worker process 29
2024/12/11 14:43:20 [notice] 1#1: start worker process 30
2024/12/11 14:43:20 [notice] 1#1: start worker process 31
2024/12/11 14:43:20 [notice] 1#1: start worker process 32
2024/12/11 14:43:20 [notice] 1#1: start worker process 33
2024/12/11 14:43:20 [notice] 1#1: start worker process 34
2024/12/11 14:43:20 [notice] 1#1: start worker process 35
2024/12/11 14:43:20 [notice] 1#1: start worker process 36
```
afficher toutes les informations relatives au conteneur avec une commande docker inspect
```
matis@thinkpad:~$ docker inspect sad_easley 
[
    {
        "Id": "ef5a6168f3fe6789a29377baa11cc1b04425a9dfa0c3987ac9836c3c42954116",
        "Created": "2024-12-11T14:43:19.771355319Z",
        "Path": "/docker-entrypoint.sh",
        "Args": [
            "nginx",
            "-g",
            "daemon off;"
        ],
        "State": {
            "Status": "running",
            "Running": true,
            "Paused": false,
            "Restarting": false,
            "OOMKilled": false,
            "Dead": false,
            "Pid": 10309,
            "ExitCode": 0,
            "Error": "",
            "StartedAt": "2024-12-11T14:43:20.389291262Z",
            "FinishedAt": "0001-01-01T00:00:00Z"
        },
        "Image": "sha256:66f8bdd3810c96dc5c28aec39583af731b34a2cd99471530f53c8794ed5b423e",
        "ResolvConfPath": "/var/lib/docker/containers/ef5a6168f3fe6789a29377baa11cc1b04425a9dfa0c3987ac9836c3c42954116/resolv.conf",
        "HostnamePath": "/var/lib/docker/containers/ef5a6168f3fe6789a29377baa11cc1b04425a9dfa0c3987ac9836c3c42954116/hostname",
        "HostsPath": "/var/lib/docker/containers/ef5a6168f3fe6789a29377baa11cc1b04425a9dfa0c3987ac9836c3c42954116/hosts",
        "LogPath": "/var/lib/docker/containers/ef5a6168f3fe6789a29377baa11cc1b04425a9dfa0c3987ac9836c3c42954116/ef5a6168f3fe6789a29377baa11cc1b04425a9dfa0c3987ac9836c3c42954116-json.log",
        "Name": "/sad_easley",
        "RestartCount": 0,
        "Driver": "overlay2",
        "Platform": "linux",
        "MountLabel": "",
        "ProcessLabel": "",
        "AppArmorProfile": "docker-default",
        "ExecIDs": null,
        "HostConfig": {
            "Binds": null,
            "ContainerIDFile": "",
            "LogConfig": {
                "Type": "json-file",
                "Config": {}
            },
            "NetworkMode": "bridge",
            "PortBindings": {
                "80/tcp": [
                    {
                        "HostIp": "",
                        "HostPort": "9999"
                    }
                ]
            },
            "RestartPolicy": {
                "Name": "no",
                "MaximumRetryCount": 0
            },
            "AutoRemove": false,
            "VolumeDriver": "",
            "VolumesFrom": null,
            "ConsoleSize": [
                41,
                154
            ],
            "CapAdd": null,
            "CapDrop": null,
            "CgroupnsMode": "private",
            "Dns": [],
            "DnsOptions": [],
            "DnsSearch": [],
            "ExtraHosts": null,
            "GroupAdd": null,
            "IpcMode": "private",
            "Cgroup": "",
            "Links": null,
            "OomScoreAdj": 0,
            "PidMode": "",
            "Privileged": false,
            "PublishAllPorts": false,
            "ReadonlyRootfs": false,
            "SecurityOpt": null,
            "UTSMode": "",
            "UsernsMode": "",
            "ShmSize": 67108864,
            "Runtime": "runc",
            "Isolation": "",
            "CpuShares": 0,
            "Memory": 0,
            "NanoCpus": 0,
            "CgroupParent": "",
            "BlkioWeight": 0,
            "BlkioWeightDevice": [],
            "BlkioDeviceReadBps": [],
            "BlkioDeviceWriteBps": [],
            "BlkioDeviceReadIOps": [],
            "BlkioDeviceWriteIOps": [],
            "CpuPeriod": 0,
            "CpuQuota": 0,
            "CpuRealtimePeriod": 0,
            "CpuRealtimeRuntime": 0,
            "CpusetCpus": "",
            "CpusetMems": "",
            "Devices": [],
            "DeviceCgroupRules": null,
            "DeviceRequests": null,
            "MemoryReservation": 0,
            "MemorySwap": 0,
            "MemorySwappiness": null,
            "OomKillDisable": null,
            "PidsLimit": null,
            "Ulimits": [],
            "CpuCount": 0,
            "CpuPercent": 0,
            "IOMaximumIOps": 0,
            "IOMaximumBandwidth": 0,
            "MaskedPaths": [
                "/proc/asound",
                "/proc/acpi",
                "/proc/kcore",
                "/proc/keys",
                "/proc/latency_stats",
                "/proc/timer_list",
                "/proc/timer_stats",
                "/proc/sched_debug",
                "/proc/scsi",
                "/sys/firmware",
                "/sys/devices/virtual/powercap"
            ],
            "ReadonlyPaths": [
                "/proc/bus",
                "/proc/fs",
                "/proc/irq",
                "/proc/sys",
                "/proc/sysrq-trigger"
            ]
        },
        "GraphDriver": {
            "Data": {
                "LowerDir": "/var/lib/docker/overlay2/814ff07d9f3424a48c0a563b51d568ef045c59c595179dbcf48b9c97fc2aca22-init/diff:/var/lib/docker/overlay2/c39532130be41e02924112bb3f31dce1ca479be3b842e4ecbfbb23f2804a016b/diff:/var/lib/docker/overlay2/c6b95667ec0a75edbb7a49f49a67f93e8ede462d196e3667d2efdc85612ffc35/diff:/var/lib/docker/overlay2/10699b83bc951959b234186ec7c08a23456341256ffdf51b4037a35bae23f999/diff:/var/lib/docker/overlay2/9d97d6d1b10e55daaaa8d4da328128ab209b45cf4a7b29c3c06fe31f3ef0da46/diff:/var/lib/docker/overlay2/4eaaef445ff422900393c6f77491b2c6a6f2efdc06bee7f660ac31d7d51e16e9/diff:/var/lib/docker/overlay2/321753b19828ab0a7dbbfdadea3c6d562c98478fdca20b77feb52b3ebe9376ff/diff:/var/lib/docker/overlay2/344942b85eaab7a89004965b3d2f3bfb31b1c46a57741d718a9dded6070177d7/diff",
                "MergedDir": "/var/lib/docker/overlay2/814ff07d9f3424a48c0a563b51d568ef045c59c595179dbcf48b9c97fc2aca22/merged",
                "UpperDir": "/var/lib/docker/overlay2/814ff07d9f3424a48c0a563b51d568ef045c59c595179dbcf48b9c97fc2aca22/diff",
                "WorkDir": "/var/lib/docker/overlay2/814ff07d9f3424a48c0a563b51d568ef045c59c595179dbcf48b9c97fc2aca22/work"
            },
            "Name": "overlay2"
        },
        "Mounts": [],
        "Config": {
            "Hostname": "ef5a6168f3fe",
            "Domainname": "",
            "User": "",
            "AttachStdin": false,
            "AttachStdout": false,
            "AttachStderr": false,
            "ExposedPorts": {
                "80/tcp": {}
            },
            "Tty": false,
            "OpenStdin": false,
            "StdinOnce": false,
            "Env": [
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin",
                "NGINX_VERSION=1.27.3",
                "NJS_VERSION=0.8.7",
                "NJS_RELEASE=1~bookworm",
                "PKG_RELEASE=1~bookworm",
                "DYNPKG_RELEASE=1~bookworm"
            ],
            "Cmd": [
                "nginx",
                "-g",
                "daemon off;"
            ],
            "Image": "nginx",
            "Volumes": null,
            "WorkingDir": "",
            "Entrypoint": [
                "/docker-entrypoint.sh"
            ],
            "OnBuild": null,
            "Labels": {
                "maintainer": "NGINX Docker Maintainers <docker-maint@nginx.com>"
            },
            "StopSignal": "SIGQUIT"
        },
        "NetworkSettings": {
            "Bridge": "",
            "SandboxID": "f1a8da69c4481c4426a6dbb9821bae3762b73762f89026f3e5aba343dbd405f9",
            "SandboxKey": "/var/run/docker/netns/f1a8da69c448",
            "Ports": {
                "80/tcp": [
                    {
                        "HostIp": "0.0.0.0",
                        "HostPort": "9999"
                    },
                    {
                        "HostIp": "::",
                        "HostPort": "9999"
                    }
                ]
            },
            "HairpinMode": false,
            "LinkLocalIPv6Address": "",
            "LinkLocalIPv6PrefixLen": 0,
            "SecondaryIPAddresses": null,
            "SecondaryIPv6Addresses": null,
            "EndpointID": "39b9d6d9e466a39433944d5f13142a1d928c8ae28042c61dae5b4f28a1e2ada8",
            "Gateway": "172.17.0.1",
            "GlobalIPv6Address": "",
            "GlobalIPv6PrefixLen": 0,
            "IPAddress": "172.17.0.2",
            "IPPrefixLen": 16,
            "IPv6Gateway": "",
            "MacAddress": "02:42:ac:11:00:02",
            "Networks": {
                "bridge": {
                    "IPAMConfig": null,
                    "Links": null,
                    "Aliases": null,
                    "MacAddress": "02:42:ac:11:00:02",
                    "DriverOpts": null,
                    "NetworkID": "85534193742d8e89b1bd779bae1273f4f2260b07b0905a1830595f9f132c3818",
                    "EndpointID": "39b9d6d9e466a39433944d5f13142a1d928c8ae28042c61dae5b4f28a1e2ada8",
                    "Gateway": "172.17.0.1",
                    "IPAddress": "172.17.0.2",
                    "IPPrefixLen": 16,
                    "IPv6Gateway": "",
                    "GlobalIPv6Address": "",
                    "GlobalIPv6PrefixLen": 0,
                    "DNSNames": null
                }
            }
        }
    }
]
```
afficher le port en écoute sur la VM avec un sudo ss -lnpt
```
matis@thinkpad:~$ sudo ss -lnpt 
State   Recv-Q   Send-Q          Local Address:Port      Peer Address:Port  Process                                                                     
LISTEN  0        1024                127.0.0.1:1123           0.0.0.0:*      users:(("TabNine",pid=6961,fd=71))                                         
LISTEN  0        100                 127.0.0.1:49152          0.0.0.0:*      users:(("TabNine-deep-lo",pid=7176,fd=14))                                 
LISTEN  0        4096                127.0.0.1:9050           0.0.0.0:*      users:(("tor",pid=1438,fd=6))                                              
LISTEN  0        5                   127.0.0.1:705            0.0.0.0:*      users:(("snmpd",pid=2251,fd=12))                                           
LISTEN  0        128                 127.0.0.1:631            0.0.0.0:*      users:(("cupsd",pid=1350,fd=7))                                            
LISTEN  0        4096                  0.0.0.0:9999           0.0.0.0:*      users:(("docker-proxy",pid=10228,fd=4))                                    
LISTEN  0        128                 127.0.0.1:38701          0.0.0.0:*      users:(("vdb",pid=7601,fd=13))                                             
LISTEN  0        4096            127.0.0.53%lo:53             0.0.0.0:*      users:(("systemd-resolve",pid=1161,fd=14))                                 
LISTEN  0        5                     0.0.0.0:902            0.0.0.0:*      users:(("vmware-authdlau",pid=2854,fd=9))                                  
LISTEN  0        128                   0.0.0.0:22             0.0.0.0:*      users:(("sshd",pid=1411,fd=4))                                             
LISTEN  0        4096                127.0.0.1:8081           0.0.0.0:*      users:(("bettercap",pid=4898,fd=10))                                       
LISTEN  0        4096       [::ffff:127.0.0.1]:41633                *:*      users:(("jetbrains-toolb",pid=4658,fd=87))                                 
LISTEN  0        50         [::ffff:127.0.0.1]:52829                *:*      users:(("jetbrains-toolb",pid=4658,fd=86))                                 
LISTEN  0        128                     [::1]:631               [::]:*      users:(("cupsd",pid=1350,fd=6))                                            
LISTEN  0        4096                     [::]:9999              [::]:*      users:(("docker-proxy",pid=10264,fd=4))                                    
LISTEN  0        5                        [::]:902               [::]:*      users:(("vmware-authdlau",pid=2854,fd=8))                                  
LISTEN  0        128                      [::]:22                [::]:*      users:(("sshd",pid=1411,fd=3)) 
```
ouvrir le port 9999/tcp (vu dans le ss au dessus normalement) dans le firewall de la VM
```
matis@thinkpad:~$ sudo iptables -A INPUT -p tcp --dport 9999 -j ACCEPT
matis@thinkpad:~$ sudo ss -lnpt
State   Recv-Q   Send-Q          Local Address:Port      Peer Address:Port  Process                                                                     
LISTEN  0        1024                127.0.0.1:1123           0.0.0.0:*      users:(("TabNine",pid=6961,fd=71))                                         
LISTEN  0        100                 127.0.0.1:49152          0.0.0.0:*      users:(("TabNine-deep-lo",pid=7176,fd=14))                                 
LISTEN  0        4096                127.0.0.1:9050           0.0.0.0:*      users:(("tor",pid=1438,fd=6))                                              
LISTEN  0        5                   127.0.0.1:705            0.0.0.0:*      users:(("snmpd",pid=2251,fd=12))                                           
LISTEN  0        128                 127.0.0.1:631            0.0.0.0:*      users:(("cupsd",pid=1350,fd=7))                                            
LISTEN  0        4096                  0.0.0.0:9999           0.0.0.0:*      users:(("docker-proxy",pid=10228,fd=4))                                    
LISTEN  0        128                 127.0.0.1:38701          0.0.0.0:*      users:(("vdb",pid=7601,fd=13))                                             
LISTEN  0        4096            127.0.0.53%lo:53             0.0.0.0:*      users:(("systemd-resolve",pid=1161,fd=14))                                 
LISTEN  0        5                     0.0.0.0:902            0.0.0.0:*      users:(("vmware-authdlau",pid=2854,fd=9))                                  
LISTEN  0        128                   0.0.0.0:22             0.0.0.0:*      users:(("sshd",pid=1411,fd=4))                                             
LISTEN  0        4096                127.0.0.1:8081           0.0.0.0:*      users:(("bettercap",pid=4898,fd=10))                                       
LISTEN  0        4096       [::ffff:127.0.0.1]:41633                *:*      users:(("jetbrains-toolb",pid=4658,fd=87))                                 
LISTEN  0        50         [::ffff:127.0.0.1]:52829                *:*      users:(("jetbrains-toolb",pid=4658,fd=86))                                 
LISTEN  0        128                     [::1]:631               [::]:*      users:(("cupsd",pid=1350,fd=6))                                            
LISTEN  0        4096                     [::]:9999              [::]:*      users:(("docker-proxy",pid=10264,fd=4))                                    
LISTEN  0        5                        [::]:902               [::]:*      users:(("vmware-authdlau",pid=2854,fd=8))                                  
LISTEN  0        128                      [::]:22                [::]:*      users:(("sshd",pid=1411,fd=3))
```
depuis le navigateur de votre PC, visiter le site web sur http://IP_VM:9999
```
matis@thinkpad:~$ curl http://10.33.65.138:9999
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
html { color-scheme: light dark; }
body { width: 35em; margin: 0 auto;
font-family: Tahoma, Verdana, Arial, sans-serif; }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
```

🌞 On va ajouter un site Web au conteneur NGINX

```
matis@thinkpad:~$ docker run -d -p 9999:8080 -v /home/matis/nginx/index.html:/var/www/html/index.html -v /home/matis/nginx/site_nul.conf:/etc/nginx/conf.d/site_nul.conf nginx
a818c279210d4746f4fcedfe5145fb411636aafe4ba24f7acde593d91a521a52
docker: Error response from daemon: driver failed programming external connectivity on endpoint laughing_wing (b810a7072ed16b7c88a89848cb71530750c2c81d2bfbc8e1c3ee10df0e013e28): Bind for 0.0.0.0:9999 failed: port is already allocated.
```

🌞 Visitons

vérifier que le conteneur est actif
```
matis@thinkpad:~$ docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS          PORTS                                     NAMES
ef5a6168f3fe   nginx     "/docker-entrypoint.…"   20 minutes ago   Up 20 minutes   0.0.0.0:9999->80/tcp, [::]:9999->80/tcp   sad_easley

```

## 3. Un deuxième conteneur en vif

🌞 Lance un conteneur Python, avec un shell

```
matis@thinkpad:~$ docker run -it python bash 
Unable to find image 'python:latest' locally
latest: Pulling from library/python
fdf894e782a2: Pull complete 
5bd71677db44: Pull complete 
551df7f94f9c: Pull complete 
ce82e98d553d: Pull complete 
5f0e19c475d6: Pull complete 
abab87fa45d0: Pull complete 
2ac2596c631f: Pull complete 
Digest: sha256:220d07595f288567bbf07883576f6591dad77d824dce74f0c73850e129fa1f46
Status: Downloaded newer image for python:latest
root@3b3585212abe:/# 
```
🌞 Installe des libs Python

```
root@3b3585212abe:/# pip install aiohttp
Requirement already satisfied: aiohttp in /usr/local/lib/python3.13/site-packages (3.11.10)
Requirement already satisfied: aiohappyeyeballs>=2.3.0 in /usr/local/lib/python3.13/site-packages (from aiohttp) (2.4.4)
Requirement already satisfied: aiosignal>=1.1.2 in /usr/local/lib/python3.13/site-packages (from aiohttp) (1.3.1)
Requirement already satisfied: attrs>=17.3.0 in /usr/local/lib/python3.13/site-packages (from aiohttp) (24.2.0)
Requirement already satisfied: frozenlist>=1.1.1 in /usr/local/lib/python3.13/site-packages (from aiohttp) (1.5.0)
Requirement already satisfied: multidict<7.0,>=4.5 in /usr/local/lib/python3.13/site-packages (from aiohttp) (6.1.0)
Requirement already satisfied: propcache>=0.2.0 in /usr/local/lib/python3.13/site-packages (from aiohttp) (0.2.1)
Requirement already satisfied: yarl<2.0,>=1.17.0 in /usr/local/lib/python3.13/site-packages (from aiohttp) (1.18.3)
Requirement already satisfied: idna>=2.0 in /usr/local/lib/python3.13/site-packages (from yarl<2.0,>=1.17.0->aiohttp) (3.10)
WARNING: Running pip as the 'root' user can result in broken permissions and conflicting behaviour with the system package manager, possibly rendering your system unusable.It is recommended to use a virtual environment instead: https://pip.pypa.io/warnings/venv. Use the --root-user-action option if you know what you are doing and want to suppress this warning.
root@3b3585212abe:/# python3
Python 3.13.1 (main, Dec  4 2024, 20:40:27) [GCC 12.2.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import aiohttp
>>> 
>>> 
KeyboardInterrupt
>>> exit
root@3b3585212abe:/# 

```
