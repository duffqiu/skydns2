# skydns2
docker file for [skydns2](https://github.com/skynetservices/skydns) base on centos 7

### some knows about skydns

- the domain must under /skydns directory in etcd
- only support one domain, if you setup multiple domain, skydns will run confusion
- the NS record must in the directory of /skydns/<your domain>/dns. For example, for the domain duffqiu.org, the name server1:ns1 must set in /skydns/org/duffqiu/dns/ns1. you can add more record under the dns directory.
- Unit file to configure the data of skydns must use `etcdctl` command, don't use the restful interface with curl
- the hostname in the SRV/A record must longer than 2 letters.

### skydns container

- don't use `-d` to run the container
- if you use global systemd unit, you need to make sure the hostname of docker host must be uneque.
- for the global systemd uint, you need to go to the host to check the log with systemctl/journalctl because fleetctl doesn't support to check the global unit logs.

### some notes about fleetctl

- must run `eval \`ssh-agent\` ` , and user `ssh-addd` to add your private key to ssh-agent. otherwise you can't access other docker host in the coreos cluster
- it is better to have a look at systemd unit spec. don't trust the example in the internet overhead
- you can use `{1..n}` to start mutiple services. for example, start 3 service `{1..3}`
