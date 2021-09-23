---
description: Uses the Graphene Framework and C++.
---

# Graphene

## Quickstart

Follow our [Graphene GitHub repository](https://github.com/DEIPworld/deip-graphene) to get started 🛠️

Just want to get up and running quickly? Try deploying a prebuilt dockerized container. Both common binary types are included.

### Dockerized p2p node

To run a p2p node \(around 2GB of memory is required at the moment\):

```text
docker run \
    -d -p 2001:2001 -p 8090:8090 --name deipd-default \
    deip/deip

docker logs -f deipd-default  # follow along
```

### Dockerized full node

To run a node with _all_  the data \(e.g. for supporting a content website\) that uses around 14GB of memory and growing:

```text
docker run \
    --env USE_WAY_TOO_MUCH_RAM=1 --env USE_FULL_WEB_NODE=1 \
    -d -p 2001:2001 -p 8090:8090 --name deipd-full \
    deip/deip

docker logs -f deipd-full
```

## Environment variables

There are quite a few environment variables that can be set to run deipd in different ways:

* `USE_WAY_TOO_MUCH_RAM` - if set to true, deipd starts a 'full node'
* `USE_FULL_WEB_NODE` - if set to true, a default config file will be used that enables a full set of API and associated plugins
* `USE_NGINX_FRONTEND` - if set to true, this will enable an NGINX reverse proxy in front of deipd that proxies WebSocket requests to deipd; this will also enable a custom health check at the path '/health' that lists how many seconds away from the current blockchain time your node is; it will return a '200' if it's less than 60 seconds away from sync
* `USE_MULTICORE_READONLY` - if set to true, this will enable deipd in multiple reader modes to take advantage of multiple cores \(if available\); read requests are handled by the read-only nodes and write requests are forwarded back to the single 'writer' node automatically; NGINX load balances all requests to the reader nodes, 4 per available core; this setting is still considered experimental and may have trouble with some API calls until further development is completed
* `HOME` - set this to the path where you want deipd to store its data files \(block log, shared memory, config file, etc.\); by default /var/lib/deipd is used and exists inside the docker container; if you want to use a different mountpoint \(like a ramdisk, or a different drive\) then you may want to set this variable to map the volume to your docker container

## PaaS mode

Deipd now supports a PaaS \(platform-as-a-service\) model that currently works with Amazon's Elastic Beanstalk service. It can be launched using the following environment variables:

* `USE_PAAS` - if set to true, deipd will launch in a format that works with AWS EB; containers will exit upon failure so that they can be relaunched automatically by ECS; this mode assumes `USE_WAY_TOO_MUCH_RAM` and `USE_FULL_WEB_NODE`, which also don't need to be set
* `S3_BUCKET` - set this to the name of the S3 bucket where you will store shared memory files for deipd in Amazon S3; they will be stored compressed in bz2 format with the file name `blockchain-$VERSION-latest.tar.bz2`, where $VERSION is the release number followed by the git short commit hash stored in each docker image at `/etc/deipdversion`
* `SYNC_TO_S3` - if set to true, the node will function to only generate shared memory files and upload them to the specified S3 bucket; this makes fast deployments and autoscaling for deipd possible

## Seed nodes

See a [list of some seed nodes](https://github.com/DEIPworld/deip-graphene/commit/4192e63d59ba863a8ec0886849f7e69811b506ed#diff-5cf34724d0c2fdbe10032483aa0eb6ca3c8e4df1950befe8fd72e8a4183421c4) to get you started.

This same file is baked into the docker images and can be overridden by setting `DEIPD_SEED_NODES` in the container environment at `docker run` time to a whitespace delimited list of seed nodes \(with port\).

## Building

See [doc/building.md](https://github.com/DEIPworld/deip-graphene/blob/develop/doc/building.md) for detailed build instructions, including compile-time options, and specific commands for Linux \(Ubuntu LTS\) or macOS X:

{% page-ref page="building.md" %}

## Testing

See [doc/testing.md](https://github.com/DEIPworld/deip-graphene/blob/develop/doc/testing.md) for test build targets and info on how to use lcov to check code test coverage:

{% page-ref page="testing.md" %}

## Develop

See [doc/develop.mp](https://github.com/DEIPworld/deip-graphene/blob/develop/doc/develop.md) for development instructions:

{% page-ref page="develop.md" %}

## System requirements

For a full web node, you need at least 55GB of space available. Deipd uses a memory mapped file which currently holds 36GB of data and by default is set to use up to 40GB. The block log of the blockchain itself is a little over 10GB. It's highly recommended to run deipd on a fast disk such as an SSD or by placing the shared memory files in a ramdisk and using the `--shard-file-dir=/path` command line option to specify where. At least 16GB of memory is required for a full web node. Seed nodes \(p2p mode\) can run with as little as 4GB of memory. Any CPU with decent single core performance should be sufficient.

On Linux use the following Virtual Memory configuration for the initial sync and subsequent replays. It is not needed for normal operation.

```text
echo    75 | sudo tee /proc/sys/vm/dirty_background_ratio
echo  1000 | sudo tee /proc/sys/vm/dirty_expire_centisec
echo    80 | sudo tee /proc/sys/vm/dirty_ratio
echo 30000 | sudo tee /proc/sys/vm/dirty_writeback_centisec
```

