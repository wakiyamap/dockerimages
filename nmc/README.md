Official Blocknet Bitcoin Images
=================================

These namecoin docker images can be found on the docker hub: https://hub.docker.com/r/blocknetdx/namecoin/

namecoin
========

These namecoin images are optimized for use with the Blocknet DX.

**Note**

These images are _not a replacement or endorsement_ of the namecoin project (https://github.com/namecoin/namecoin-core).


Simple
======

Run a simple namecoin node on port 8334:
```
docker run -d --name=namecoin -p 8334:8334 blocknetdx/namecoin:latest
```


Persist blockchain w/ volumes
=============================

Run a namecoin node that persists the blockchain on a host directory. Recommended to avoid time consuming resyncs when updating to later container versions.
```
docker run -d --name=namecoin -p 8334:8334 -v=/crypto/namecoin/config:/opt/blockchain/config -v=/crypto/namecoin/data:/opt/blockchain/data blocknetdx/namecoin:0.17.0.1
```


Automatically restart the container
===================================

See https://docs.docker.com/engine/admin/start-containers-automatically/

`--restart=no|on-failure:retrycount|always|unless-stopped`

```
docker run -d --restart=no --name=namecoin -p 8334:8334 blocknetdx/namecoin:0.17.0.1 namecoind -daemon=0 -rpcuser=nmc -rpcpassword=nmc123
docker run -d --restart=on-failure:10 --name=namecoin -p 8334:8334 blocknetdx/namecoin:0.17.0.1 namecoind -daemon=0 -rpcuser=nmc -rpcpassword=nmc123
docker run -d --restart=unless-stopped --name=bitcoin -p 8334:8334 blocknetdx/namecoin:0.17.0.1 namecoind -daemon=0 -rpcuser=nmc -rpcpassword=nmc123
docker run -d --restart=always --name=bitcoin -p 8334:8334 blocknetdx/namecoin:0.17.0.1 namecoind -daemon=0 -rpcuser=nmc -rpcpassword=nmc123
```


Container shell access
======================

To login to the namecoin container and run RPC commands use the following command:
```
docker exec -it namecoin /bin/bash
```


Default namecoin.conf
=====================

The default configuration is below. A custom configuration file can be passed to the namecoin  node container through the `/opt/blockchain/config` volume. Some of these parameters can also be adjusted on the command line.
```
datadir=/opt/blockchain/data

dbcache=256
maxmempool=512

port=8333    # testnet: 18333
rpcport=8332 # testnet: 18332

listen=1
server=1
logtimestamps=1
logips=1

rpcallowip=127.0.0.1
rpctimeout=15
rpcclienttimeout=15
```


License
=======

This code is licensed under the Apache 2.0 License. Please refer to the [LICENSE](https://github.com/BlocknetDX/dockerimages/blob/master/LICENSE).