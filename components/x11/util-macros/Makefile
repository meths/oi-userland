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
#

include ../../../make-rules/shared-macros.mk

COMPONENT_NAME= util-macros
COMPONENT_VERSION= 1.17.1
COMPONENT_SUMMARY= GNU autoconf macros for X.Org software packages
COMPONENT_SRC= $(COMPONENT_NAME)-$(COMPONENT_VERSION)
COMPONENT_ARCHIVE= $(COMPONENT_SRC).tar.gz
COMPONENT_ARCHIVE_HASH= \
  sha256:67bd01d5f4713c9e9d57dc742504d06292dd9c4fb73041ea16fed034c56c622a
COMPONENT_ARCHIVE_URL= \
  http://ftp.x.org/pub/individual/util/$(COMPONENT_ARCHIVE)
COMPONENT_PROJECT_URL = https://x.org

include $(WS_TOP)/make-rules/prep.mk
include $(WS_TOP)/make-rules/configure.mk
include $(WS_TOP)/make-rules/ips.mk

COMPONENT_PREP_ACTION =        ( cd $(@D)  && autoreconf -f )

CONFIGURE_OPTIONS += --sysconfdir=/etc

build: $(BUILD_32)

install: $(INSTALL_32)
