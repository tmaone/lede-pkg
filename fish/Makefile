#
# Copyright (C) 2011-2017 Entware
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=fish
PKG_VERSION:=2.6.0
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://github.com/fish-shell/fish-shell/releases/download/2.6.0
PKG_MD5SUM:=ce9d8cc2a34d172a94cfa3ef9988937c
PKG_INSTALL:=1

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk

define Package/fish
	SECTION:=shells
	CATEGORY:=Base system
	TITLE:=A smart and user-friendly command line shell
	DEPENDS:=+libncurses +libstdcpp +coreutils-whoami
	URL:=https://fishshell.com
endef

define Package/fish/description
 Fish is a smart and user-friendly command line shell for OS X, Linux, and the rest of the family.
 Fish includes features like syntax highlighting, autosuggest-as-you-type, and fancy tab completions that just work,
 with no configuration required.
endef

# CONFIGURE_VARS += ac_cv_file__proc_self_stat=yes
# MAKE_FLAGS += EXTRA_CXXFLAGS=" -I$(STAGING_DIR)/opt/include"
#define Package/fish/conffiles
#/opt/etc/fish.conf
#endef

define Build/Configure
	$(call Build/Configure/Default, \
		--bindir=/bin \
		--prefix=/usr )
endef

define Package/fish/postinst
#!/bin/sh
grep fish $${IPKG_INSTROOT}/etc/shells || \
  echo "/bin/fish" >> $${IPKG_INSTROOT}/etc/shells
endef

define Package/fish/install
	$(INSTALL_DIR) $(1)/bin
	$(CP) $(PKG_INSTALL_DIR)/bin/* $(1)/bin
	$(CP) ./files/apropos $(1)/usr/bin/
	$(INSTALL_DIR) $(1)/usr/etc/fish/conf.d
	$(CP) ./files/config.fish $(1)/usr/etc/fish/
	$(INSTALL_DIR) $(1)/usr/share/fish
	$(CP) $(PKG_INSTALL_DIR)/usr/share/fish/* $(1)/usr/share/fish/
	rm -rf $(1)/opt/share/fish/groff
	#rm -rf $(1)/opt/share/fish/man
	#rm -rf $(1)/opt/share/fish/tools
endef

$(eval $(call BuildPackage,fish))
