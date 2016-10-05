include $(TOPDIR)/rules.mk

PKG_NAME:=ffhgw-banner
PKG_VERSION:=1
PKG_RELEASE:=1

PKG_BUILD_DIR := $(BUILD_DIR)/$(PKG_NAME)

include $(INCLUDE_DIR)/package.mk

define Package/ffhgw-banner
  SECTION:=ffhgw
  CATEGORY:=Customization
  TITLE:=Banner file replacement
  DEPENDS:=+gluon-core +busybox
endef

define Package/ffhgw-banner/description
	Banner file replacement
endef

define Build/Prepare
	mkdir -p $(PKG_BUILD_DIR)
endef

define Build/Configure
endef

define Build/Compile
endef

define Package/ffhgw-banner/preinst
#!/bin/sh
cd "$${IPKG_INSTROOT}/etc/"
if [ -h "./banner" ] ; then
	/bin/rm "./banner"
elif [ -f "./banner" ] ; then
	/bin/mv "./banner" "./banner.openwrt"
fi
/bin/ln -s "./banner.openwrt" "./banner"
exit 0
endef

define Package/ffhgw-banner/postinst
#!/bin/sh
cd "$${IPKG_INSTROOT}/etc/"
[ -h "./banner" ] && /bin/rm -f "./banner"
/bin/ln -s "./banner.ffhgw" "./banner"
exit $$?
endef

define Package/ffhgw-banner/prerm
#!/bin/sh
cd "$${IPKG_INSTROOT}/etc/"
if [ -h "./banner" ] ; then
	[[ "$$(readlink -n ./banner)" == "./banner.ffhgw" ]] && \
	/bin/rm -f "./banner" && \
	[ -f "./banner.openwrt" ] && \
	/bin/ln -s "./banner.openwrt" "./banner"
fi
exit 0
endef

define Package/ffhgw-banner/install
	$(INSTALL_DIR) $(1)/etc/
	$(INSTALL_DATA) ./files/etc/banner.ffhgw $(1)/etc/
endef

$(eval $(call BuildPackage,ffhgw-banner))
