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

2021.09

