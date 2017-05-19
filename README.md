## Logspout is an easy way to ship logs.

# Usage
```
docker-compse up -d
```

# The quick and dirty to send logs from all docker containers to logstash

```
docker run --restart=always --detach=true --name="logspout" --volume=/var/run/docker.sock:/var/run/docker.sock gliderlabs/logspout syslog+tcp://logstash:5000
```

# Important

The vm_max_map_count kernel setting needs to be set to at least 262144. Depending on your platform:

* Linux
  * The vm_map_max_count setting should be set permanently in /etc/sysctl.conf:
```
$ grep vm.max_map_count /etc/sysctl.conf
vm.max_map_count=262144
```
  * To apply the setting on a live system type:
```
sysctl -w vm.max_map_count=262144
```

* OSX with Docker for Mac
  * The vm_max_map_count setting must be set within the xhyve virtual machine:
```
$ screen ~/Library/Containers/com.docker.docker/Data/com.docker.driver.amd64-linux/tty
```
  * Log in with root and no password. Then configure the sysctl setting as you would for Linux:
```
sysctl -w vm.max_map_count=262144
```
* OSX with Docker Toolbox
  * The vm_max_map_count setting must be set via docker-machine:
```
docker-machine ssh
sudo sysctl -w vm.max_map_count=262144
```


More info,

https://www.elastic.co/guide/en/elasticsearch/reference/current/docker.html
