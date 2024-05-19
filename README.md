

## build env

use docker

### build docker image. run once
```bash
git clone https://github.com/KunYi/uboot-ipq60xx-build
cd uboot-ipq60xx-build
cd docker
./build.sh
cd ..
```

### build

u-boot-2016 source code base on https://github.com/gl-inet/uboot-ipq60xx and
https://github.com/0x5826/uboot-ipq60xx-build

```bash
./entrycontainer
./build.sh
exit
```

The uboot binary will be: uboot-ipq60xx-build/u-boot.mbn

The uboot failsafe HTTP server ip: 192.168.1.1
