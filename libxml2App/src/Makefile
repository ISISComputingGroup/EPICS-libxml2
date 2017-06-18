TOP=../..

include $(TOP)/configure/CONFIG

#ifneq ($(findstring windows,$(EPICS_HOST_ARCH)),)

ifneq ($(findstring debug,$(EPICS_HOST_ARCH)),)
CDEBUG=yes
ifeq ($(STATIC_BUILD),YES)
CRUNTIME=/MTd /DEPICS_DLL_NO
else
CRUNTIME=/MDd /DEPICS_BUILD_DLL 
endif
else
CDEBUG=no
ifeq ($(STATIC_BUILD),YES)
CRUNTIME=/MT /DEPICS_DLL_NO
else
CRUNTIME=/MD /DEPICS_BUILD_DLL 
endif
endif
USE_ZLIB=yes

include $(TOP)/configure/RULES

ifdef T_A
install:
	$(MAKE) -C $(TOP)/libxml2-2.9.2/win32 -f Makefile.epics install T_A=$(T_A) CDEBUG=$(CDEBUG) CRUNTIME="$(CRUNTIME)" USE_ZLIB=$(USE_ZLIB) TOP=$(LIBXML2)
ifeq ($(OS_CLASS),WIN32)
	$(CP) $(TOP)/lib/$(T_A)/libxml2.lib $(TOP)/lib/$(T_A)/xml2.lib
endif
endif

ifeq ($(BASE_3_14),YES)
clean:: myclean
else
clean: myclean
endif

myclean:
	$(MAKE) -C $(TOP)/libxml2-2.9.2/win32 -f Makefile.epics clean

uninstall:
