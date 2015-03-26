include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/kernel.mk


RUBY_PKG_LIBVER:=1.9

PKG_NAME:=ruby-eventmachine
PKG_RELEASE:=1
PKG_REV:=master
PKG_VERSION:=$(PKG_REV)

PKG_SOURCE:=$(PKG_NAME).tar.gz
PKG_SOURCE_URL:=git://github.com/eventmachine/eventmachine.git
PKG_SOURCE_VERSION:=$(PKG_REV)
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_PROTO:=git

PKG_BUILD_DEPENDS:=ruby/host

include $(INCLUDE_DIR)/host-build.mk
include $(INCLUDE_DIR)/nls.mk

include $(INCLUDE_DIR)/package.mk

define Package/ruby-eventmachine/Default
  SUBMENU:=Ruby
  SECTION:=lang
  CATEGORY:=Languages
  TITLE:=Ruby eventmachine gem
endef

define Package/ruby-eventmachine
  $(call Package/ruby-eventmachine/Default)
  DEPENDS:=ruby +libstdcpp +libc +libgcc +ruby-fastfilereader
  TITLE:=(event machine)
endef

define Package/ruby-fastfilereader
  $(call Package/ruby-eventmachine/Default)
  DEPENDS:=ruby +libstdcpp +libc +libgcc
  TITLE:=(event machine fastfilereader)
endef

RUBY:= \
	$(STAGING_DIR_HOST)/bin/ruby -I $(STAGING_DIR_HOST)/share/ri \

define Package/ruby-eventmachine/description
 This package contains the ruby eventmachine gem.
endef

define Build/ruby-eventmachine/Configure
	(cd $(PKG_BUILD_DIR)/ext; \
		$(RUBY) extconf.rb; \
	);
endef

define Build/ruby-eventmachine/Compile
	+$(MAKE_VARS) \
	$(MAKE) $(PKG_JOBS) -C $(PKG_BUILD_DIR)/ext \
		$(MAKE_FLAGS) \
		$(1);
endef

define Build/ruby-fastfilereader/Configure
	(cd $(PKG_BUILD_DIR)/ext/fastfilereader; \
		$(RUBY) extconf.rb; \
	);
endef

define Build/ruby-fastfilereader/Compile
	+$(MAKE_VARS) \
	$(MAKE) $(PKG_JOBS) -C $(PKG_BUILD_DIR)/ext/fastfilereader \
		$(MAKE_FLAGS) \
		$(1);
endef

#define Build/Configure
#	$(call Build/Configure/eventmachine)
#	$(call Build/Configure/fastfilereader)
#endef
#
#define Build/Compile
#	$(call Build/Compile/fastfilereader)
#	$(call Build/Compile/eventmachine)
#endef

#define Package/ruby-eventmachine/install
#	$(INSTALL_DIR) $(1)/usr/lib/ruby/site_ruby/1.9/mips-linux
#	$(CP) $(PKG_BUILD_DIR)/lib/eventmachine.rb $(1)/usr/lib/ruby/site_ruby/1.9/
#	$(CP) $(PKG_BUILD_DIR)/lib/em $(1)/usr/lib/ruby/site_ruby/1.9/
#	$(CP) $(PKG_BUILD_DIR)/lib/*.so $(1)/usr/lib/ruby/site_ruby/1.9/mips-linux
#endef


define Package/ruby-eventmachine/install
	$(INSTALL_DIR) $(1)/usr/lib/ruby/$(PKG_LIBVER)
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/ruby/eventmachine.rb $(1)/usr/lib/ruby/$(PKG_LIBVER)/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/ruby/em $(1)/usr/lib/ruby/$(PKG_LIBVER)/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/ruby/*.so $(1)/usr/lib/ruby/$(PKG_LIBVER)/
endef

define Package/ruby-fastfilereader/install
	$(INSTALL_DIR) $(1)/usr/lib/ruby/$(PKG_LIBVER)
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/ruby/eventmachine.rb $(1)/usr/lib/ruby/$(PKG_LIBVER)/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/ruby/em $(1)/usr/lib/ruby/$(PKG_LIBVER)/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/ruby/*.so $(1)/usr/lib/ruby/$(PKG_LIBVER)/
endef

#define Package/ruby-eventmachine/install
#	$(INSTALL_DIR) $(1)/usr/lib/ruby/site_ruby/1.9/mips-linux
#	$(CP) $(PKG_BUILD_DIR)/lib/eventmachine.rb $(1)/usr/lib/ruby/site_ruby/1.9/
#	$(CP) $(PKG_BUILD_DIR)/lib/em $(1)/usr/lib/ruby/site_ruby/1.9/
#	$(CP) $(PKG_BUILD_DIR)/lib/*.so $(1)/usr/lib/ruby/site_ruby/1.9/mips-linux
#endef

$(eval $(call BuildPackage,ruby-eventmachine))
$(eval $(call BuildPackage,ruby-fastfilereader))
$(eval $(call HostBuild))
