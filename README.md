# openwrt-docker

Ubuntu docker develop env for OpenWRT.

## Usage

Build docker image:

```bash
docker build -t ubuntu:openwrt -f Dockerfile .
```

Run docker to build OpenWRT:

```bash
docker run --rm -it ubuntu:openwrt bash
```

To [configure and build](https://oldwiki.archive.openwrt.org/doc/howto/build#image_configuration):

```bash
make menuconfig 
make
```

## HiWifi HC5661

Build OpenWRT for HiWifi HC5661, [Lenovo Y1](https://openwrt.org/toh/lenovo/y1?s[]=lenovo&s[]=y1).

```bash
docker build -t ubuntu:openwrt-hiwifi_y1 -f Dockerfile.openwrt-hiwifi_y1 .
```

Run docker to build package for HiWifi:

```bash
docker run --rm -it -v `pwd`:/output ubuntu:openwrt-hiwifi_y1 bash
```

## Basic Ubuntu 20 LTS(Focal Fossa)

Prepare the Ubuntu 20 LTS(Focal Fossa), without OpenWRT.

```bash
docker build -t ubuntu:openwrt-basic-ubuntu20 -f Dockerfile.openwrt-basic-ubuntu20 .
```

## Build package srs-router

Run docker, which mount current directory to volume `/output`:

```bash
docker run --rm -it -v `pwd`:/output ubuntu:openwrt-hiwifi_y1 bash
```

Create feed for `ossrs`, update and install package `srs-router`:

```bash
cp /output/openwrt-srs-router-feeds.conf feeds.conf.default
./scripts/feeds update ossrs
./scripts/feeds install srs-router
```

Copy the config, or run `make menuconfig`, enable the `Multilemedia -> srs-router`, then build package `srs-router`:

```bash
cp /output/openwrt-hiwifi_y1-srs-router.config .config
make package/srs-router/compile V=s
```

Install `bin/packages/*/ossrs/srs-router_*.ipk` to OpenWRT.

Finally, run it:

```bash
root@OpenWrt:~# srs-router 
Hello OpenWRT+SRS
```

2021.09

