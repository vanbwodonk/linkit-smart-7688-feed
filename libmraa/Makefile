include $(TOPDIR)/rules.mk

PKG_NAME:=libmraa
PKG_VERSION:=1.9.0

PKG_RELEASE=$(PKG_SOURCE_VERSION)

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/intel-iot-devkit/mraa.git
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_VERSION:=fbb7d9232067eac3f4508a37a8f7ea0c4fcebacb
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION)-$(PKG_SOURCE_VERSION).tar.gz
PKG_BUILD_DEPENDS:=libjson-c node python/host swig/host node/host
CMAKE_INSTALL:=1

PKG_MAINTAINER:=John Crispin <blogic@openwrt.org>
PKG_LICENSE:=LGPL-2.1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

CMAKE_OPTIONS=-DBUILDARCH=$(CONFIG_ARCH) \
	-DENABLEEXAMPLES=0 \
	-DNODE_EXECUTABLE=$(STAGING_DIR_HOSTPKG)/bin/node \
	-DSWIG_DIR=$(STAGING_DIR_HOSTPKG)/bin
#	-DBUILDSWIG=OFF \

TARGET_CFLAGS+=-I$(STAGING_DIR)/usr/include/node

define Package/libmraa
  SECTION:=libs
  CATEGORY:=Libraries
  DEPENDS:=+python +libstdcpp +libjson-c
  TITLE:=Intel IoT lowlevel IO library
endef

define Package/libmraa/install
	$(INSTALL_DIR) $(1)/usr/lib/{node/mraa,python2.7/site-packages} $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/lib/libmraa.so* $(1)/usr/lib/
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/lib/node_modules/mraa/* $(1)/usr/lib/node/mraa/
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/lib/python2.7/site-packages/* $(1)/usr/lib/python2.7/site-packages/
#	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/share/mraa/examples/python/blink-io8.py $(1)/usr/bin/
endef

$(eval $(call BuildPackage,libmraa))