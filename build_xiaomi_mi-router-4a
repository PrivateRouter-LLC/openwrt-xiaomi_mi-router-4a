#!/bin/bash

OUTPUT="$(pwd)/images"
BUILD_VERSION="22.03.0"
BOARD_NAME="ramips"
BOARD_SUBNAME="mt7621"
BUILDER="https://downloads.openwrt.org/releases/${BUILD_VERSION}/targets/${BOARD_NAME}/${BOARD_SUBNAME}/openwrt-imagebuilder-${BUILD_VERSION}-${BOARD_NAME}-${BOARD_SUBNAME}.Linux-x86_64.tar.xz"
BASEDIR=$(realpath "$0" | xargs dirname)

# download image builder
if [ ! -f "${BUILDER##*/}" ]; then
	wget "$BUILDER"
	tar xJvf "${BUILDER##*/}"
fi

[ -d "${OUTPUT}" ] || mkdir "${OUTPUT}"

cd openwrt-*/

# clean previous images
make clean

make image  PROFILE="xiaomi_mi-router-4a-gigabit" \
           PACKAGES="luci dnsmasq" \
           FILES="${BASEDIR}/files/" \
           BIN_DIR="$OUTPUT"
