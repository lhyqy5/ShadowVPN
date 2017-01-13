include $(TOPDIR)/rules.mk

PKG_NAME:=ShadowVPN
PKG_VERSION:=0.2.1
PKG_RELEASE=$(shell LC_ALL=C git rev-parse --short HEAD)

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION)-$(PKG_RELEASE).tar.gz
PKG_SOURCE_URL:=https://github.com/lhyqy5/ShadowVPN
PKG_SOURCE_PROTO:=git
PKG_SOURCE_SUBDIR:=ShadowVPN
PKG_SOURCE_VERSION:=master

PKG_MAINTAINER:=clowwindy <clowwindy42@gmail.com>
PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=LICENSE

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)

PKG_INSTALL:=1
PKG_FIXUP:=autoreconf
PKG_USE_MIPS16:=0
PKG_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/package.mk

define Package/ShadowVPN/Default
  SECTION:=net
  CATEGORY:=Network
  TITLE:=ShadowVPN
  DEPENDS:=+kmod-tun +ip
  URL:=https://github.com/clowwindy/ShadowVPN
endef

define Package/ShadowVPN
  $(call Package/ShadowVPN/Default)
endef

define Package/ShadowVPN/description
A fast, safe VPN based on libsodium
endef

define Package/ShadowVPN/conffiles
/etc/shadowvpn/client.conf
/etc/shadowvpn/client_up.sh
/etc/shadowvpn/client_down.sh
endef

define Package/ShadowVPN/install
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_DIR) $(1)/etc/shadowvpn
	$(INSTALL_DIR) $(1)/etc/hotplug.d/iface
	$(INSTALL_CONF) $(PKG_BUILD_DIR)/samples/client.conf $(1)/etc/shadowvpn/client.conf
	$(INSTALL_CONF) $(PKG_BUILD_DIR)/samples/client_up.sh $(1)/etc/shadowvpn/client_up.sh
	$(INSTALL_CONF) $(PKG_BUILD_DIR)/samples/client_down.sh $(1)/etc/shadowvpn/client_down.sh
	$(INSTALL_CONF) $(PKG_BUILD_DIR)/samples/30-shadowvpn $(1)/etc/hotplug.d/iface/30-shadowvpn
	$(INSTALL_BIN) ./files/shadowvpn.init $(1)/etc/init.d/shadowvpn
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/shadowvpn $(1)/usr/bin
endef

$(eval $(call BuildPackage,ShadowVPN))
