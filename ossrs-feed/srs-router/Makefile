include $(TOPDIR)/rules.mk

PKG_NAME:=srs-router
PKG_VERSION:=1.0.0
PKG_RELEASE:=1

PKG_MAINTAINER:=Winlin<winlin@vip.126.com>
PKG_LICENSE:=MIT

include $(INCLUDE_DIR)/package.mk

define Package/srs-router
	SECITON:=multimedia
	CATEGORY:=Multimedia
	TITLE:=SRS router for live publisher
endef

define Package/srs-router/description
	SRS router for live publisher
endef

define Build/Prepare
	mkdir -p $(PKG_BUILD_DIR)
	$(CP) ./src/* $(PKG_BUILD_DIR)/
endef

define Package/srs-router/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/srs-router $(1)/usr/bin/
endef

$(eval $(call BuildPackage,srs-router))

