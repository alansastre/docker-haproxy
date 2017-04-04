# HAProxy Load Balancer
[![CircleCI Build Status](https://img.shields.io/circleci/project/million12/docker-haproxy/master.svg)](https://circleci.com/gh/million12/docker-haproxy)  (latest)  
[![GitHub Open Issues](https://img.shields.io/github/issues/million12/docker-haproxy.svg)](https://github.com/million12/docker-haproxy/issues)
[![GitHub Stars](https://img.shields.io/github/stars/million12/docker-haproxy.svg)](https://github.com/million12/docker-haproxy)
[![GitHub Forks](https://img.shields.io/github/forks/million12/docker-haproxy.svg)](https://github.com/million12/docker-haproxy)  
[![Stars on Docker Hub](https://img.shields.io/docker/stars/million12/haproxy.svg)](https://hub.docker.com/r/million12/haproxy)
[![Pulls on Docker Hub](https://img.shields.io/docker/pulls/million12/haproxy.svg)](https://hub.docker.com/r/million12/haproxy)  
[![](https://images.microbadger.com/badges/version/million12/haproxy.svg)](http://microbadger.com/images/million12/haproxy)
[![](https://images.microbadger.com/badges/license/million12/haproxy.svg)](http://microbadger.com/images/million12/haproxy)
[![](https://images.microbadger.com/badges/image/million12/haproxy.svg)](http://microbadger.com/images/million12/haproxy)


HAProxy docker container [million12/haproxy](https://registry.hub.docker.com/u/million12/haproxy/) with ALPN and HTTP/2 support.

##### Build status (latest versions)
* `million12/haproxy:latest` - [![CircleCI Build Status](https://img.shields.io/circleci/project/million12/docker-haproxy/master.svg)](https://circleci.com/gh/million12/docker-haproxy)  
* `million12/haproxy:1.6.4` - [![CircleCI Build Status](https://img.shields.io/circleci/project/million12/docker-haproxy/1.6.4.svg)](https://circleci.com/gh/million12/docker-haproxy)  

# Features

* **Support for HTTP/2** with ALPN
* CentOS 7 based
* Ability to **provide any arguments to haproxy** process  
  Any extra parameters provided to `docker run` will be passed directly to `haproxy` command.  
  For example, if you run `docker run [run options] million12/haproxy -n 1000` you pass `-n 1000` to haproxy daemon.
* Pretty **lightweight**, only ~290M (with OpenSSL and HAProxy compiled from source).
* **Default [haproxy.cfg](container-files/etc/haproxy/haproxy.cfg) provided** for demonstration purposes. You can easily mount your own or point to different location using `HAPROXY_CONFIG` env.
* **Auto restart when config changes**  
  This container comes with inotify to monitor changes in HAProxy config and **reload** HAProxy daemon. The reload is done in a way that no connection is lost.


## ENV variables

**HAPROXY_CONFIG**  
Default: `HAPROXY_CONFIG=/etc/haproxy/haproxy.cfg`  
If you mount your config to different location, simply edit it.


## Usage

### Basic

`docker run -ti -p 80:80 -p 443:443 million12/haproxy`

### Mount custom config , override some options

`docker run -d -p 80:80 -v /my-haproxy.cfg:/etc/haproxy/haproxy.cfg million12/haproxy -n 10000`  
Note: in this case config is mounted to its default location, so you don't need to modify `HAPROXY_CONFIG` variable.

### Check version and build options

`docker run -ti million12/haproxy -vv`

### Stats
The default URL for stats is `http://CONTAINER_IP/admin?stats` with username:password ser to `admin:admin`.

## Authors

Author: Marcin ryzy Ryzycki (<marcin@m12.io>)  
Author: Przemyslaw Ozgo (<linux@ozgo.info>)
