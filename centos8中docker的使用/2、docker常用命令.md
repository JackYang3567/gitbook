# docker常用命令
```
简单将docker命令分为下列4类：
1、帮助命令
2、镜像命令
3、容器命令
4、监控命令
```

## 1、帮助命令

### 1.1、version显示docker的版本信息
```
$ docker version 

Client: Docker Engine - Community
 Version:           20.10.14
 API version:       1.41
 Go version:        go1.16.15
 Git commit:        a224086
 Built:             Thu Mar 24 01:47:44 2022
 OS/Arch:           linux/amd64
 Context:           default
 Experimental:      true

Server: Docker Engine - Community
 Engine:
  Version:          20.10.14
  API version:      1.41 (minimum version 1.12)
  Go version:       go1.16.15
  Git commit:       87a90dc
  Built:            Thu Mar 24 01:46:10 2022
  OS/Arch:          linux/amd64
  Experimental:     false
 containerd:
  Version:          1.5.11
  GitCommit:        3df54a852345ae127d1fa3092b95168e4a88e2f8
 runc:
  Version:          1.0.3
  GitCommit:        v1.0.3-0-gf46b6ba
 docker-init:
  Version:          0.19.0
  GitCommit:        de40ad0
```
### 1.2、info显示docker的系统信息，包括镜像和容器的数量
```
$ docker info   

Client:
 Context:    default
 Debug Mode: false
 Plugins:
  app: Docker App (Docker Inc., v0.9.1-beta3)
  buildx: Docker Buildx (Docker Inc., v0.8.1-docker)
  scan: Docker Scan (Docker Inc., v0.17.0)

Server:
 Containers: 0
  Running: 0
  Paused: 0
  Stopped: 0
 Images: 1
 Server Version: 20.10.14
 Storage Driver: overlay2
  Backing Filesystem: xfs
  Supports d_type: true
  Native Overlay Diff: true
  userxattr: false
 Logging Driver: json-file
 Cgroup Driver: cgroupfs
 Cgroup Version: 1
 Plugins:
  Volume: local
  Network: bridge host ipvlan macvlan null overlay
  Log: awslogs fluentd gcplogs gelf journald json-file local logentries splunk syslog
 Swarm: inactive
 Runtimes: io.containerd.runtime.v1.linux runc io.containerd.runc.v2
 Default Runtime: runc
 Init Binary: docker-init
 containerd version: 3df54a852345ae127d1fa3092b95168e4a88e2f8
 runc version: v1.0.3-0-gf46b6ba
 init version: de40ad0
 Security Options:
  seccomp
   Profile: default
 Kernel Version: 4.18.0-348.7.1.el8_5.x86_64
 Operating System: CentOS Linux 8
 OSType: linux
 Architecture: x86_64
 CPUs: 2
 Total Memory: 1.774GiB
 Name: centos8.localdomain
 ID: W3GI:4WEN:FWZP:DD5T:BIZP:CYBJ:ZKKB:QCQD:7YEQ:MFID:GEU5:QEN7
 Docker Root Dir: /var/lib/docker
 Debug Mode: false
 Registry: https://index.docker.io/v1/
 Labels:
 Experimental: false
 Insecure Registries:
  127.0.0.0/8
 Registry Mirrors:
  https://wixr7yss.mirror.aliyuncs.com/
 Live Restore Enabled: false
```

### 1.3、命令 --help 帮助命令
```
$ docker version --help

Usage:  docker version [OPTIONS]

Show the Docker version information

Options:
  -f, --format string       Format the output using the given Go template
      --kubeconfig string   Kubernetes config file
 
```

## 2、镜像命令


## 3、容器命令


## 4、监控命令