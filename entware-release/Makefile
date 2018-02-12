#
# Copyright (C) 2011-2017 Entware
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# This is the same package as entware-opt, it does not install busybox. It makes several symlinks instead of it!
# /opt/... folder order in /opt/etc/profile is different, /opt folders are the last in PATH
# This package is a replacement of entware-opt for asuswrt firmware


include $(TOPDIR)/rules.mk

PKG_NAME:=entware-release
PKG_VERSION:=1.0
PKG_RELEASE:=1

include $(INCLUDE_DIR)/package.mk

define Package/entware-release
	SECTION:=base
	CATEGORY:=Base system
	TITLE:=Entware relese information
	MAINTAINER:=Entware team, http://entware.net
endef

define Package/entware-release/description
 entware_release is a file in /opt/etc with entware info
endef

define Build/Prepare
endef

define Build/Configure
endef

define Build/Compile
endef

define Package/entware-release/install
	$(INSTALL_DIR) $(1)/opt/etc/
endef

CPU=$(if $(CONFIG_CPU_TYPE),$(CONFIG_CPU_TYPE),unknown)
CPUSUBTYPE=$(if $(CONFIG_CPU_SUBTYPE),$(CONFIG_CPU_SUBTYPE),unknown)
FLOAT=$(if $(CONFIG_SOFT_FLOAT),soft,hard)

ENVCFLAGS:=$(TARGET_OPTIMIZATION) $(call qstrip,$(CONFIG_EXTRA_OPTIMIZATION))
ifeq ($(CONFIG_SOFT_FLOAT),y)
    ifeq ($(CONFIG_arm),y)
        ENVCFLAGS+= -mfloat-abi=soft
    else
        ENVCFLAGS+= -msoft-float
    endif
endif

LIBCTYPE=$(if $(CONFIG_LIBC_USE_GLIBC),glibc,uclibc-ng)



define Package/entware-release/postinst
#!/bin/sh
echo "release=entware-3x" > /opt/etc/entware_release
echo "arch=$(ARCH)" >> /opt/etc/entware_release
echo "cpu=$(call qstrip,$(CPU))" >> /opt/etc/entware_release
echo "cpu_subtype=$(CPUSUBTYPE)" >> /opt/etc/entware_release
echo "float=$(FLOAT)" >> /opt/etc/entware_release
echo "gcc=$(call qstrip,$(CONFIG_GCC_VERSION))" >> /opt/etc/entware_release
echo "gcc_flags=$(ENVCFLAGS)" >> /opt/etc/entware_release
echo "libc=$(LIBCTYPE)" >> /opt/etc/entware_release
echo "libc_version=$(call qstrip,$(CONFIG_GLIBC_VERSION))" >> /opt/etc/entware_release
endef

$(eval $(call BuildPackage,entware-release))