include $(TOPDIR)/rules.mk

PKG_NAME:=srs-server
PKG_VERSION:=5.0.16
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://github.com/ossrs/srs/releases/download/v$(PKG_VERSION)
PKG_HASH:=3aa90f2a9939e49be29e020a03f69bf6

PKG_MAINTAINER:=Winlin <winlin@vip.126.com>
PKG_LICENSE:=MIT

include $(INCLUDE_DIR)/package.mk

define Package/srs-server
	SECITON:=multimedia
	CATEGORY:=Multimedia
	DEPENDS:=+libstdcpp +libopenssl
	TITLE:=SRS Simple Realtime Server
endef

define Package/srs-server/description
	SRS Simple Realtime Server
endef

# Strip off FPU notation
REAL_CPU_TYPE:=$(firstword $(subst +, ,$(CONFIG_CPU_TYPE)))
# Fixup cpu types recogized by ffmpeg configure
REAL_CPU_TYPE:=$(subst octeonplus,octeon+,$(REAL_CPU_TYPE))

SRS_CONFIGURE:=\
	CFLAGS="$(TARGET_CFLAGS) $(TARGET_CPPFLAGS) $(FPIC)"\
	LDFLAGS="$(TARGET_LDFLAGS)" \
	./configure \
	--cross-build \
	--cross-prefix=$(TARGET_CROSS) \
	--arch=$(ARCH) \
	$(if $(REAL_CPU_TYPE),--cpu=$(call qstrip,$(REAL_CPU_TYPE)),)

# Disable some features of SRS.
SRS_CONFIGURE+=--rtc=off
SRS_CONFIGURE+=--ffmpeg-fit=off
SRS_CONFIGURE+=--nasm=off --srtp-nasm=off
SRS_CONFIGURE+=--cxx11=off
SRS_CONFIGURE+=--sys-ssl=on

# Disable the mprotect of ST, because it cause segment fault.
SRS_CONFIGURE+=--extra-flags="-DMD_NO_PROTECT"

# Config the make jobs.
SRS_CONFIGURE+=$(if $(PKG_JOBS),--jobs=$(shell echo $(PKG_JOBS)| sed 's/^-j//g'| sed 's/^--jobs=//g'),)

define Build/Configure
	( cd $(PKG_BUILD_DIR)/trunk && $(SRS_CONFIGURE) )
endef

define Build/Compile
	+$(MAKE) $(PKG_JOBS) -C $(PKG_BUILD_DIR)/trunk \
		DESTDIR="$(PKG_INSTALL_DIR)" \
		server
	+$(MAKE) $(PKG_JOBS) -C $(PKG_BUILD_DIR)/trunk \
		DESTDIR="$(PKG_INSTALL_DIR)" \
		install
endef

define Package/srs-server/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/trunk/objs/srs $(1)/usr/bin/srs-server
	$(INSTALL_DIR) $(PKG_BUILD_DIR)/trunk/conf $(1)/etc/srs/conf
	$(CP) $(PKG_BUILD_DIR)/trunk/conf/*.conf $(1)/etc/srs/conf/
endef

$(eval $(call BuildPackage,srs-server))

