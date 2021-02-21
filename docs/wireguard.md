### key generation

```shell
$ (umask 0077; wg genkey | tee privatekey | wg pubkey > privatekey)
```

- creation happen in a sub-shell to make sure it's restricted to the owner
- umask is use to strip these permissions when creation

### wg-quick

`wg-quick` configures `/etc/wireguard/interfacename.conf`

`wg-quick` add more configurations to the file, so it's not compatible with `wg` format now. Get the wg-compatible configuration by `wg-quick strip`.

Be sure no other networking management tools are trying to modify these configuration, like `NetworkManager`.

