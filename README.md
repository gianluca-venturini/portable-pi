### Sources
- OpenWRT image builder: https://openwrt.org/docs/guide-user/additional-software/imagebuilder
- Wireless overview https://openwrt.org/docs/guide-quick-start/basic_wifi

diskutil erasevolume HFSX "openwrt" `hdiutil attach -nomount ram://4194304`
docker run -it --entrypoint /bin/bash --mount=type=bind,source=/Volumes/openwrt,target=/openwrt/ debian@sha256:5a12d4d61ffc727a1343bfed7ef1327e7dfa499483e9458ef9c48e7a990b3e64

apt-get update
apt install -y build-essential libncurses5-dev libncursesw5-dev zlib1g-dev gawk git gettext libssl-dev xsltproc rsync wget unzip python python3
apt-get clean

cd /openwrt
wget https://downloads.openwrt.org/snapshots/targets/bcm27xx/bcm2711/openwrt-imagebuilder-bcm27xx-bcm2711.Linux-x86_64.tar.xz
tar -J -x -f openwrt-imagebuilder-*.tar.xz
make image PACKAGES="kmod-rt2800-lib kmod-rt2800-usb kmod-rt2x00-lib kmod-rt2x00-usb kmod-usb-core kmod-usb-uhci kmod-usb-ohci kmod-usb2 usbutils openvpn-openssl luci-app-openvpn"