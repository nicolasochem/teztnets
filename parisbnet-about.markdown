---
layout: page
title: ParisBnet
permalink: /parisbnet-about
---

Exploratory Chain for Paris B protocol

| | |
|-------|---------------------|
| Public RPC endpoints | [https://rpc.parisbnet.teztnets.com](https://rpc.parisbnet.teztnets.com/chains/main/chain_id)<br/> |
| Faucet | [ParisBnet faucet](https://faucet.parisbnet.teztnets.com) |
| Full network name | `TEZOS_PARIS_B_NET_2024-04-02T18:00:00Z` |
| Tezos docker build | [tezos/tezos:octez-v20.0-beta2](https://hub.docker.com/r/tezos/tezos/tags?page=1&ordering=last_updated&name=octez-v20.0-beta2) |
| Activated on | 2024-03-27T15:00:00Z |





### Install the software

⚠️  If you already have an existing Tezos installation, do not forget to backup and delete your `~/.tezos-node` and `~/.tezos-client`.



#### Alternative: Use docker

To join ParisBnet with docker, open a shell in the container:

```
docker run -it --entrypoint=/bin/sh tezos/tezos:octez-v20.0-beta2
```

#### Alternative: Build the software

⚠️  If this is your first time installing Tezos, you may need to [install a few dependencies](https://tezos.gitlab.io/introduction/howtoget.html#setting-up-the-development-environment-from-scratch).

```
cd
git clone git@gitlab.com:tezos/tezos.git
cd tezos
git checkout octez-v20.0-beta2
opam init # if this is your first time using OPAM
make build-deps
eval $(opam env)
make
export PATH=$HOME/tezos:$PATH
```

### Join the ParisBnet network

Run the following commands:

```
octez-node config init --network https://teztnets.com/parisbnet

octez-node run --rpc-addr 127.0.0.1:8732
```






### Bake on the ParisBnet network

To improve reliability of the chain, you can take part in the consensus by becoming a baker. In that case, you will need some test tokens from the [faucet](https://faucet.parisbnet.teztnets.com).

If you are not a bootstrap baker, you need to register your key as a delegate using your alias or `pkh`. For instance:
```bash=2
octez-client register key mykey as delegate
```

You may now launch the baker process.
```bash=3
octez-baker-PtParisB run with local node ~/.tezos-node mykey --liquidity-baking-toggle-vote pass
```

You may run the accuser as well:
```bash=3
octez-accuser-PtParisB run
```

Note that you need a minimum amount of tez to get baking rights. If you are not a bootstrap baker, it will take you several cycles to start baking.

> 💡 Now that you are baking, you are responsible for the network health. Please ensure that the baking processes will keep running in the background. You may want to use screen, tmux, nohup or systemd. Also make sure that the baking processes will restart when your machine restarts.


