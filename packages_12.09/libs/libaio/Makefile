#
# Copyright (C) 2007-2010 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=libaio
PKG_VERSION:=0.3.107
PKG_RELEASE:=2

PKG_SOURCE:=$(PKG_NAME)_$(PKG_VERSION).orig.tar.gz
PKG_SOURCE_URL:=http://ftp.debian.org/debian/pool/main/liba/libaio/
PKG_MD5SUM:=db32c19c61ca937bcb1ba48da9180682

include $(INCLUDE_DIR)/package.mk

define Package/libaio
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=Linux kernel AIO interface access library
  URL:=http://lse.sourceforge.net/io/aio.html
endef

define Build/Configure
endef

LIBAIO_CFLAGS:=-nostdlib -nostartfiles -I. $(TARGET_CFLAGS) $(TARGET_CPPFLAGS) $(FPIC)

TARGET_CFLAGS += $(FPIC)

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR) \
		$(TARGET_CONFIGURE_OPTS) \
		ARCH="$(ARCH)" \
		CC="$(TARGET_CROSS)gcc" \
		LD="$(TARGET_CROSS)ld" \
		CFLAGS="$(LIBAIO_CFLAGS)" \
		all
	$(MAKE) -C $(PKG_BUILD_DIR) \
		prefix="$(PKG_INSTALL_DIR)/usr" \
		install
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include
	$(CP) $(PKG_INSTALL_DIR)/usr/include/libaio.h $(1)/usr/include/
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libaio.{a,so*} $(1)/usr/lib/
endef

define Package/libaio/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libaio.so.* $(1)/usr/lib/
endef

$(eval $(call BuildPackage,libaio))
