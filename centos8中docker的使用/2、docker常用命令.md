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
### 2.1、docker search 搜索镜像
####  2.1.1、docker search详解
```
$ docker search --help


Usage:  docker search [OPTIONS] TERM

Search the Docker Hub for images

Options:
  -f, --filter filter   Filter output based on conditions provided
      --format string   Pretty-print search using a Go template
      --limit int       Max number of search results (default 25)
      --no-trunc        Don't truncate output


用法：docker search[选项]术语（镜像名称）

在Docker Hub中搜索镜像


选项：

-f、--filter filter 根据提供的条件过滤输出

--format string  使用Go模板格式化字符串打印搜索

--limit int  限制int最大搜索结果数（默认值25）

--no-trunc  不截断输出
```
####  2.1.2、docker search实例
```
$ docker search gitlab

NAME                                   DESCRIPTION                                     STARS     OFFICIAL   AUTOMATED
gitlab/gitlab-ce                       GitLab Community Edition docker image based …   3564                 [OK]
gitlab/gitlab-runner                   GitLab CI Multi Runner used to fetch and run…   776                  [OK]
gitlab/gitlab-ee                       GitLab Enterprise Edition docker image based…   314
gitlab/gitlab-runner-helper                                                            36
gitlab/dind                            The image is deprecated and will be not upda…   33                   [OK]
gitlab/gitlab-ce-qa                    GitLab QA has a test suite that allows end-t…   7
bitnami/gitlab-runner                                                                  5
gitlab/cog                             GitLab Bundle for Cog                           4
gitlab/gitlab-dns                      Managing GitLab's External DNS                  2
gitlab/gitlab-ee-qa                    GitLab QA has a test suite that allows end-t…   2
gitlab/postgres                        Allows GitLab employees to send read only qu…   2
gitlab/gitlab-performance-tool         GitLab QA performance test tool - https://gi…   1
gitlab/pagerbot                                                                        1
gitlab/ssh-tunnel                      https://gitlab.com/gitlab-org/quality/ssh-tu…   1
gitlabelinvar/dind                     dind                                            0
gitlab/gitlab-qa                       GitLab QA has a test suite that allows end-t…   0
gitlabtools/gitlab-ldap-group-sync                                                     0
gitlab/cog_chef                                                                        0
okteto/gitlab                                                                          0
bitnami/gitlab-runner-helper                                                           0
gitlab/gpt-data-generator              The GPT Data Generator creates all test data…   0
gitlab/ymir                                                                            0
gitlabcibuild/test-elastic-image       See https://gitlab.com/gitlab-org/test-elast…   0
circleci/gitlab-single-org-connector   CircleCI GitLab Connector Demonstration         0
gitlab/gitlab-agent-ci-image           CI image for verifying and testing the gitla…   0
```

### 2.2、docker pull 拉取镜像

####  2.2.1、docker pull详解
```
$ docker pull --help



Usage:  docker pull [OPTIONS] NAME[:TAG|@DIGEST]

Pull an image or a repository from a registry

Options:
  -a, --all-tags                Download all tagged images in the repository
      --disable-content-trust   Skip image verification (default true)
      --platform string         Set platform if server is multi-platform capable
  -q, --quiet                   Suppress verbose output
```
####  2.2.2、docker pull实例
```
$ docker pull gitlab/gitlab-ce

Using default tag: latest
latest: Pulling from gitlab/gitlab-ce
7b1a6ab2e44d: Pull complete                                                                                                              6c37b8f20a77: Pull complete                                                                                                              f50912690f18: Pull complete                                                                                                              bb6bfd78fa06: Pull complete                                                                                                              2c03ae575fcd: Pull complete                                                                                                              839c111a7d43: Pull complete                                                                                                              4989fee924bc: Pull complete                                                                                                              666a7fb30a46: Pull complete                                                                                                              
Digest: sha256:5a0b03f09ab2f2634ecc6bfeb41521d19329cf4c9bbf330227117c048e7b5163
Status: Downloaded newer image for gitlab/gitlab-ce:latest
docker.io/gitlab/gitlab-ce:latest
```


### 2.3、docker images 显示镜像
####  2.3.1、docker images详解
```
$ docker images --help

Usage:  docker images [OPTIONS] [REPOSITORY[:TAG]]

List images

Options:
  -a, --all             Show all images (default hides intermediate images) 列出所镜像
      --digests         Show digests
  -f, --filter filter   Filter output based on conditions provided
      --format string   Pretty-print images using a Go template
      --no-trunc        Don't truncate output
  -q, --quiet           Only show image IDs  只显示镜像ID
```
####  2.3.2、docker images实例
```
$  docker images
REPOSITORY         TAG       IMAGE ID       CREATED        SIZE
gitlab/gitlab-ce   <none>    9c00b5927bae   7 days ago     2.45GB
gitlab/gitlab-ce   latest    46cd6954564a   3 months ago   2.36GB

## 解释
REPOSITORY 镜像的仓库源
TAG        镜像的标签
IMAGE ID   镜像id
CREATED    镜像的创建时间
SIZE       镜像的大小
```

### 2.4、docker rmi 删除镜像
####  2.4.1、docker rmi详解
```
$ docker rmi --help

Usage:  docker rmi [OPTIONS] IMAGE [IMAGE...]

Remove one or more images

Options:
  -f, --force      Force removal of the image
      --no-prune   Do not delete untagged parents
```
####  2.4.2、docker rmi实例
```
$ docker images -a
REPOSITORY         TAG       IMAGE ID       CREATED        SIZE
gitlab/gitlab-ce   <none>    9c00b5927bae   7 days ago     2.45GB
gitlab/gitlab-ce   latest    46cd6954564a   3 months ago   2.36GB

$ docker rmi 9c00b5927bae
Untagged: gitlab/gitlab-ce@sha256:b987cc1bbff2d2b70ab5dbac272be47c1df86c745451ce7b03678139101ddbe9
Deleted: sha256:9c00b5927bae442d3f8902f5c3bb58acb849fb1969d4ce85eb1699b3618729b8
Deleted: sha256:42be1455e497f72d650d0733c8207737c573c2cae909f7b1aa773c8d8175579a
Deleted: sha256:68861922570bbcb5aa5d4cc1a1b3738c397b4716a8e40e11062852e65e8cacf6
Deleted: sha256:435d920d9d868c62fbb7ff8d95c236381f5685cf89792b1c648fe3f1e82fa91a
Deleted: sha256:039dcfc3790fcefe9cfa7b4be11eaf474ff6e9b018c6af50ca2c09ef115e3845
Deleted: sha256:6c1ac826d3f3ebedc5ccb2071bb437a1438710051f2b19471ecd5d663fcd69e5
Deleted: sha256:8f21dbb06480a64f69349985e1b4741057f5b3849676c9bd5a3f05cb01463c95
Deleted: sha256:1376d7b6ab2b784ba852720933f29189c970d126654205ea11e6cc44a79bcd0a
Deleted: sha256:867d0767a47c392f80acb51572851923d6d3e55289828b0cd84a96ba342660c7
$ docker images -a
REPOSITORY         TAG       IMAGE ID       CREATED        SIZE
gitlab/gitlab-ce   latest    46cd6954564a   3 months ago   2.36GB

```

## 3、容器命令
####  3.1.1、docker run详解
```

```
####  3.1.2、docker run实例
```

```
####  3.2.1、docker ps详解
```

```

####  3.3.2、docker ps实例
```

```

####  3.3.1、docker exit详解
```

```
####  3.3.2、docker exit实例
```

```

####  3.4.1、docker rm详解
```

```
####  3.4.2、docker rm实例
```

```
####  3.5.1、docker start详解
```

```
####  3.5.2、docker start实例
```

```

####  3.6.1、docker restart详解
```

```
####  3.6.2、docker restart实例
```

```
####  3.7.1、docker stop详解
```

```
####  3.7.2、docker stop实例
```

```
####  3.8.1、docker kill详解
```

```
####  3.8.2、docker kill实例
```

```
## 4、监控命令

####  4.1、查看日志命令
#####  4.1.1、docker logs详解
```

```
#####  4.1.2、docker logs实例
```

```
####  4.2、查看容器中的进程信息
#####  4.2.1、docker top详解
```

```
#####  4.2.2、docker top实例
```

```

####  4.3、查看镜像的元数据
#####  4.3.1、docker inspect详解
```

```
#####  4.3.2、docker inspect实例
```

```

####  4.4、进入当前正在运行的容器
#####  4.4.1、docker exec详解
```

```
#####  4.4.2、docker exec实例
```

```

####  4.5、从容器内拷贝文件到主机上
#####  4.5.1、docker cp详解
```

```
#####  4.5.2、docker cp实例
```

```

## 5、更多命令
```
$ docker --help

Usage:  docker [OPTIONS] COMMAND

A self-sufficient runtime for containers

Options:
      --config string      Location of client config files (default "/root/.docker")
  -c, --context string     Name of the context to use to connect to the daemon (overrides DOCKER_HOST env var and
                           default context set with "docker context use")
  -D, --debug              Enable debug mode
  -H, --host list          Daemon socket(s) to connect to
  -l, --log-level string   Set the logging level ("debug"|"info"|"warn"|"error"|"fatal") (default "info")
      --tls                Use TLS; implied by --tlsverify
      --tlscacert string   Trust certs signed only by this CA (default "/root/.docker/ca.pem")
      --tlscert string     Path to TLS certificate file (default "/root/.docker/cert.pem")
      --tlskey string      Path to TLS key file (default "/root/.docker/key.pem")
      --tlsverify          Use TLS and verify the remote
  -v, --version            Print version information and quit

Management Commands:
  app*        Docker App (Docker Inc., v0.9.1-beta3)
  builder     Manage builds
  buildx*     Docker Buildx (Docker Inc., v0.8.1-docker)
  config      Manage Docker configs
  container   Manage containers
  context     Manage contexts
  image       Manage images
  manifest    Manage Docker image manifests and manifest lists
  network     Manage networks
  node        Manage Swarm nodes
  plugin      Manage plugins
  scan*       Docker Scan (Docker Inc., v0.17.0)
  secret      Manage Docker secrets
  service     Manage services
  stack       Manage Docker stacks
  swarm       Manage Swarm
  system      Manage Docker
  trust       Manage trust on Docker images
  volume      Manage volumes

Commands:
  attach      Attach local standard input, output, and error streams to a running container
  build       Build an image from a Dockerfile
  commit      Create a new image from a container's changes
  cp          Copy files/folders between a container and the local filesystem
  create      Create a new container
  diff        Inspect changes to files or directories on a container's filesystem
  events      Get real time events from the server
  exec        Run a command in a running container
  export      Export a container's filesystem as a tar archive
  history     Show the history of an image
  images      List images
  import      Import the contents from a tarball to create a filesystem image
  info        Display system-wide information
  inspect     Return low-level information on Docker objects
  kill        Kill one or more running containers
  load        Load an image from a tar archive or STDIN
  login       Log in to a Docker registry
  logout      Log out from a Docker registry
  logs        Fetch the logs of a container
  pause       Pause all processes within one or more containers
  port        List port mappings or a specific mapping for the container
  ps          List containers
  pull        Pull an image or a repository from a registry
  push        Push an image or a repository to a registry
  rename      Rename a container
  restart     Restart one or more containers
  rm          Remove one or more containers
  rmi         Remove one or more images
  run         Run a command in a new container
  save        Save one or more images to a tar archive (streamed to STDOUT by default)
  search      Search the Docker Hub for images
  start       Start one or more stopped containers
  stats       Display a live stream of container(s) resource usage statistics
  stop        Stop one or more running containers
  tag         Create a tag TARGET_IMAGE that refers to SOURCE_IMAGE
  top         Display the running processes of a container
  unpause     Unpause all processes within one or more containers
  update      Update configuration of one or more containers
  version     Show the Docker version information
  wait        Block until one or more containers stop, then print their exit codes

Run 'docker COMMAND --help' for more information on a command.

To get more help with docker, check out our guides at https://docs.docker.com/go/guides/
```