#
# This file and its contents are supplied under the terms of the
# Common Development and Distribution License ("CDDL"), version 1.0.
# You may only use this file in accordance with the terms of version
# 1.0 of the CDDL.
#
# A full copy of the text of the CDDL should have accompanied this
# source.  A copy of the CDDL is also available via the Internet at
# http://www.illumos.org/license/CDDL.
#

#
# Copyright 2015 Alexander Pyhalov
# Copyright 2015 Ken Mays
#

include ../../../make-rules/shared-macros.mk

COMPONENT_NAME= mesa
COMPONENT_VERSION= 11.1.2
COMPONENT_SUMMARY= The Mesa 3-D Graphics Library
COMPONENT_SRC= mesa-$(COMPONENT_VERSION)
COMPONENT_ARCHIVE= mesa-$(COMPONENT_VERSION).tar.xz
COMPONENT_ARCHIVE_HASH= \
  sha256:8f72aead896b340ba0f7a4a474bfaf71681f5d675592aec1cb7ba698e319148b
COMPONENT_ARCHIVE_URL= \
  ftp://ftp.freedesktop.org/pub/mesa/$(COMPONENT_VERSION)/$(COMPONENT_ARCHIVE)
COMPONENT_PROJECT_URL = http://www.mesa3d.org/

include $(WS_TOP)/make-rules/prep.mk
include $(WS_TOP)/make-rules/configure.mk
include $(WS_TOP)/make-rules/ips.mk

PATCH_LEVEL=0

ARCHLIBSUBDIR.64=/$(MACH64)
ARCHLIBSUBDIR=$(ARCHLIBSUBDIR.$(BITS))

SERVERMOD_SUBDIR.64=/$(MACH64)
SERVERMOD_SUBDIR=$(SERVERMOD_SUBDIR.$(BITS))
X11_SERVERMODS_DIR=/usr/lib/xorg/modules
X11_SERVERLIBS_DIR=/usr/lib/xorg

COMPONENT_POST_UNPACK_ACTION +=  ( cp -r $(COMPONENT_DIR)/srcs/* $(SOURCE_DIR) )
COMPONENT_PREP_ACTION +=  (cd $(SOURCE_DIR) && \
                                        libtoolize --copy --force &&\
                                        aclocal -I m4 &&\
                                        automake -c -f -a &&\
                                        autoconf)

CONFIGURE_SCRIPT = $(@D)/configure


# Missing files in build dir for configure without this.
COMPONENT_PRE_CONFIGURE_ACTION =        (cp -a $(SOURCE_DIR)/* $(@D) )

# Add include paths and linker paths needed for DRM modules
CPPFLAGS = -I/usr/X11/include/drm -D__EXTENSIONS__

LDFLAGS= -L$(PROTODIR)$(X11_SERVERLIBS_DIR)$(ARCHLIBSUBDIR) \
                -R$(X11_SERVERLIBS_DIR)$(ARCHLIBSUBDIR) 

LD_OPTIONS += -M $(COMPONENT_DIR)/mapfile.externs

DRI_DRIVER_LIST=i915 i965 r200 radeon swrast

# Command line options to GNU autoconf configure script
CONFIGURE_OPTIONS += --with-dri-driverdir='$(X11_SERVERMODS_DIR)/dri$(SERVERMOD_SUBDIR)'
CONFIGURE_OPTIONS += --with-dri-drivers='$(DRI_DRIVER_LIST)'
CONFIGURE_OPTIONS += --disable-gallium-llvm
CONFIGURE_OPTIONS += --disable-egl 
CONFIGURE_OPTIONS += --with-gallium-drivers=
CONFIGURE_OPTIONS += --enable-shared-glapi
CONFIGURE_OPTIONS += --enable-texture-float
CONFIGURE_OPTIONS += --enable-osmesa
CONFIGURE_OPTIONS += --sysconfdir=/etc

CONFIGURE_ENV+=PYTHON=$(PYTHON)
CONFIGURE_ENV+=CPPFLAGS="$(CPPFLAGS)"

COMPONENT_BUILD_ARGS =

build: $(BUILD_32_and_64)

install: $(INSTALL_32_and_64)
