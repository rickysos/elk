## Logspout is an easy way to ship logs.

# The quick and dirty

```
docker run --restart=always --detach=true --name="logspout" --volume=/var/run/docker.sock:/var/run/docker.sock gliderlabs/logspout syslog+tcp://logstash:5000
```
