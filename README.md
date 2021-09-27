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

## HiWifi HC5661 with USB RNDIS

Build OpenWRT for HiWifi HC5661, [Lenovo Y1](https://openwrt.org/toh/lenovo/y1?s[]=lenovo&s[]=y1).

```bash
docker build -t ubuntu:openwrt -f Dockerfile.hiwifi_hc5661-usb_rndis .
```

2021.09

