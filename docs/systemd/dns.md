### systemd-resolved

`resolvectl` can specify the DNS on the interface basis:

```shell
resolvectl dns wg0 192.168.100.101:1053
```

We can specify a simple DNS server by using CoreDNS, which will forward the DNS request:

```
# Corefile
. {
	forward . /etc/resolv.conf # do the forward
    log                        # log all requests
    errors                     # log all errors
}
```

```
./coredns
```

