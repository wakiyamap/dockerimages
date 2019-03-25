Official Blocknet Bitcoin Images
=================================

These ixcoin docker images can be found on the docker hub: https://hub.docker.com/r/blocknetdx/ixcoin/

ixcoin
========

These ixcoin images are optimized for use with the Blocknet DX.

**Note**

These images are _not a replacement or endorsement_ of the ixcoin project (https://github.com/IXCore/IXCoin).


Simple
======

Run a simple ixcoin node on port 8337:
```
docker run -d --name=ixcoin -p 8337:8337 blocknetdx/ixcoin:latest
```


Persist blockchain w/ volumes
=============================

Run a ixcoin node that persists the blockchain on a host directory. Recommended to avoid time consuming resyncs when updating to later container versions.
```
docker run -d --name=ixcoin -p 8337:8337 -v=/crypto/ixcoin/config:/opt/blockchain/config -v=/crypto/ixcoin/data:/opt/blockchain/data blocknetdx/ixcoin:0.17.0.1
```


Automatically restart the container
===================================

See https://docs.docker.com/engine/admin/start-containers-automatically/

`--restart=no|on-failure:retrycount|always|unless-stopped`

```
docker run -d --restart=no --name=ixcoin -p 8337:8337 blocknetdx/ixcoin:0.17.0.1 ixcoind -daemon=0 -rpcuser=ixc -rpcpassword=ixc123
docker run -d --restart=on-failure:10 --name=ixcoin -p 8337:8337 blocknetdx/ixcoin:0.17.0.1 ixcoind -daemon=0 -rpcuser=ixc -rpcpassword=ixc123
docker run -d --restart=unless-stopped --name=bitcoin -p 8337:8337 blocknetdx/ixcoin:0.17.0.1 ixcoind -daemon=0 -rpcuser=ixc -rpcpassword=ixc123
docker run -d --restart=always --name=bitcoin -p 8337:8337 blocknetdx/ixcoin:0.17.0.1 ixcoind -daemon=0 -rpcuser=ixc -rpcpassword=ixc123
```


Container shell access
======================

To login to the ixcoin container and run RPC commands use the following command:
```
docker exec -it ixcoin /bin/bash
```


Default ixcoin.conf
=====================

The default configuration is below. A custom configuration file can be passed to the ixcoin  node container through the `/opt/blockchain/config` volume. Some of these parameters can also be adjusted on the command line.
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