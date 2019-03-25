Official Blocknet Bitcoin Images
=================================

These magna coin docker images can be found on the docker hub: https://hub.docker.com/r/blocknetdx/magna coin/

magna coin
========

These magna coin images are optimized for use with the Blocknet DX.

**Note**

These images are _not a replacement or endorsement_ of the magna coin project (https://github.com/MagnaCoinProject/MagnaCoin).


Simple
======

Run a simple magna coin node on port 57821:
```
docker run -d --name=magna coin -p 57821:57821 blocknetdx/magna coin:latest
```


Persist blockchain w/ volumes
=============================

Run a magna coin node that persists the blockchain on a host directory. Recommended to avoid time consuming resyncs when updating to later container versions.
```
docker run -d --name=magna coin -p 57821:57821 -v=/crypto/magna coin/config:/opt/blockchain/config -v=/crypto/magna coin/data:/opt/blockchain/data blocknetdx/magna coin:0.17.0.1
```


Automatically restart the container
===================================

See https://docs.docker.com/engine/admin/start-containers-automatically/

`--restart=no|on-failure:retrycount|always|unless-stopped`

```
docker run -d --restart=no --name=magna coin -p 57821:57821 blocknetdx/magna coin:0.17.0.1 mgnd -daemon=0 -rpcuser=mgn -rpcpassword=mgn123
docker run -d --restart=on-failure:10 --name=magna coin -p 57821:57821 blocknetdx/magna coin:0.17.0.1 mgnd -daemon=0 -rpcuser=mgn -rpcpassword=mgn123
docker run -d --restart=unless-stopped --name=bitcoin -p 57821:57821 blocknetdx/magna coin:0.17.0.1 mgnd -daemon=0 -rpcuser=mgn -rpcpassword=mgn123
docker run -d --restart=always --name=bitcoin -p 57821:57821 blocknetdx/magna coin:0.17.0.1 mgnd -daemon=0 -rpcuser=mgn -rpcpassword=mgn123
```


Container shell access
======================

To login to the magna coin container and run RPC commands use the following command:
```
docker exec -it magna coin /bin/bash
```


Default mgn.conf
=====================

The default configuration is below. A custom configuration file can be passed to the magna coin  node container through the `/opt/blockchain/config` volume. Some of these parameters can also be adjusted on the command line.
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