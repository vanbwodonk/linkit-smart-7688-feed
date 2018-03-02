# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.

include $(TOPDIR)/rules.mk

PKG_NAME:=mtk-lede-linkit
PKG_RELEASE:=1

include $(INCLUDE_DIR)/package.mk

define Package/mtk-lede-linkit
	TITLE:=MTK LinkIt Smart board support package
	DEPENDS:=@TARGET_ramips_mt7688_DEVICE_LinkIt7688 \
		+gdbserver +curl +strace +coreutils +coreutils-stty \
		+avahi-nodbus-daemon \
		+block-mount +kmod-fs-ext4 +kmod-usb-storage-extras +e2fsprogs +fdisk \
		+uhttpd +rpcd +rpcd-mod-iwinfo +git +git-http +samba36-server \
		+hidapi \
		+luci +luci-app-samba +luci-lib-json \
		+rpcd-mod-rpcsys +cgi-io +avrdude +spi-tools +uboot-envtools \
		+kmod-fs-vfat +kmod-fs-exfat +kmod-i2c-core \
		+kmod-nls-base +kmod-nls-cp437 +kmod-nls-iso8859-1 \
		+kmod-nls-iso8859-15 +kmod-nls-iso8859-2 +kmod-nls-utf8 \
		+kmod-sdhci-mt7620 +kmod-usb-storage \
		+kmod-sound-core +kmod-sound-mt7620 +madplay-alsa +alsa-utils \
		+tcpdump-mini +@KERNEL_DEVMEM\

		#------remove node + phyton for smaller image---------------
		#+node +node-hid +node-cylon-firmata +yunbridge \
		#+python +python-pyserial +python-pip \

		#----generic from linkit feeds--------
		#+gdbserver +curl +strace +coreutils +coreutils-stty \
		#+avahi-nodbus-daemon +mountd +mjpg-streamer \
		#+uhttpd +rpcd +rpcd-mod-iwinfo +git +git-http +samba36-server \
		#+python +python-pyserial +python-pip +hidapi \
		#+node +node-hid +node-cylon-firmata +yunbridge \
		#+luci +luci-theme-openwrt +luci-app-mjpg-streamer +luci-app-samba +luci-lib-json \
		#+rpcd-mod-rpcsys +cgi-io +avrdude +spi-tools +uboot-envtools \
		#+kmod-fs-vfat +kmod-fs-exfat +kmod-i2c-core +kmod-i2c-ralink \
		#+kmod-nls-base +kmod-nls-cp437 +kmod-nls-iso8859-1 \
		#+kmod-nls-iso8859-15 +kmod-nls-iso8859-2 +kmod-nls-utf8 \
		#+kmod-sdhci-mt7620 +kmod-usb-storage \
		#+kmod-video-core +kmod-video-uvc \
		#+kmod-sound-core +kmod-sound-mtk +madplay-alsa +alsa-utils \
		#+mtk-lede-linkit-webui +mtk-sdk-wifi +tcpdump-mini

		#----not fail but removed--------
		#+luci-theme-openwrt +luci-app-mjpg-streamer
		#+mjpg-streamer
		#+kmod-video-core +kmod-video-uvc
		#+mtk-lede-linkit-webui +mtk-sdk-wifi

		#----fail-----------
		#+libmraa +libupm
		#+kmod-sound-mtk

	CATEGORY:=Base system
	DEFAULT:=y
endef

define Build/Prepare
	mkdir -p $(PKG_BUILD_DIR)
endef

define Build/Compile
	$(TARGET_CC) $(TARGET_CFLAGS) $(EXTRA_CFLAGS) -Wall -Werror -o $(PKG_BUILD_DIR)/pinmux src/pinmux.c ; \
	$(TARGET_CC) $(TARGET_CFLAGS) $(EXTRA_CFLAGS) -Wall -Werror -o $(PKG_BUILD_DIR)/refclk src/refclk.c
endef

define Package/mtk-lede-linkit/install
	$(INSTALL_DIR) $(1)/sbin

	$(INSTALL_BIN) $(PKG_BUILD_DIR)/pinmux $(1)/sbin/mt7688_pinmux
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/refclk $(1)/sbin/mt7688_reclk
	$(CP) ./files/* $(1)
endef

$(eval $(call BuildPackage,mtk-lede-linkit))
