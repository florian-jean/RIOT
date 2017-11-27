PKG_NAME=wakaama
PKG_URL=https://github.com/eclipse/wakaama.git
PKG_VERSION=b48e36d05ec451031514560a08e014cfb2cc81d2
#PKG_VERSION=ee80c224622684ee47c17c57918904cffd00c4d2
PKG_LICENSE=EDL-1.0,EPL-1.0

.PHONY: all

all: patch


patch: git-download
	#CANNED RECIPE CALL EXECUTED AFTER GIT-DOWNLOAD/PATCH FOR CONDITIONAL INCLUSION
	rm $(PKG_BUILDDIR)/examples/shared/dtlsconn*;
	$(add_base_makefile_wakaama)
	$(add_shared_dependency_wakaama)
	$(add_dependency_wakaama)


ifneq (,$(filter "LIGHT_CLIENT","$(WAKAAMA_EXAMPLE)"))
define add_dependency_wakaama =
	#BUILDING WAKAAMA WITH LIGHT_CLIENT
	echo BUILDING LIGHT CLIENT 
	$(add_test_light_client_dependency_wakaama)
endef

else ifneq (,$(filter "CLIENT","$(WAKAAMA_EXAMPLE)"))
define add_dependency_wakaama =
	#BUILDING WAKAAMA WITH CLIENT
	echo BUILDING CLIENT 
	$(add_test_client_dependency_wakaama)
endef

else ifneq (,$(filter "BOOTSTRAP_SERVER","$(WAKAAMA_EXAMPLE)"))
define add_dependency_wakaama =
	#BUILDING WAKAAMA WITH BOOTSTRAP_SERVER
	echo BUILDING BOOTSTRAP_SERVER
	$(add_test_bootstrap_server_dependency_wakaama)
endef

else ifneq (,$(filter "SERVER","$(WAKAAMA_EXAMPLE)"))
define add_dependency_wakaama =
	#BUILDING WAKAAMA WITH SERVER
	echo BUILDING SERVER
	$(add_test_server_dependency_wakaama)
endef
else 
define add_dependency_wakaama =
	echo BUILDING CORE ONLY
endef
endif

#DEPENDENCY FOR CLIENT
define add_test_client_dependency_wakaama =
	echo 'MODULE:=client_wakaama' > $(PKG_BUILDDIR)/examples/client/Makefile;
	echo 'CFLAGS += -I$(PKG_BUILDDIR)/examples/shared' >> $(PKG_BUILDDIR)/examples/client/Makefile;
	echo 'INCLUDE += $(RIOTPKG)/shared_wakaama' >> $(PKG_BUILDDIR)/examples/client/Makefile;
	echo 'CFLAGS += -I$(PKG_BUILDDIR)/core' >> $(PKG_BUILDDIR)/examples/client/Makefile;
	echo 'INCLUDE += $(RIOTPKG)/core_wakaama' >> $(PKG_BUILDDIR)/examples/client/Makefile;
	echo 'include $(RIOTBASE)/Makefile.base' >> $(PKG_BUILDDIR)/examples/client/Makefile;
	"$(MAKE)" -C $(PKG_BUILDDIR)/examples/client
endef

#DEPENDENCY FOR LIGHT_CLIENT
define add_test_light_client_dependency_wakaama =
	echo 'MODULE:=light_client_wakaama' > $(PKG_BUILDDIR)/examples/lightclient/Makefile;
	echo 'CFLAGS += -I$(PKG_BUILDDIR)/examples/shared' >> $(PKG_BUILDDIR)/examples/lightclient/Makefile;
	echo 'INCLUDE += $(RIOTPKG)/shared_wakaama' >> $(PKG_BUILDDIR)/examples/lightclient/Makefile;
	echo 'CFLAGS += -I$(PKG_BUILDDIR)/core' >> $(PKG_BUILDDIR)/examples/lightclient/Makefile;
	echo 'INCLUDE += $(RIOTPKG)/core_wakaama' >> $(PKG_BUILDDIR)/examples/lightclient/Makefile;
	echo 'include $(RIOTBASE)/Makefile.base' >> $(PKG_BUILDDIR)/examples/lightclient/Makefile;
	"$(MAKE)" -C $(PKG_BUILDDIR)/examples/lightclient
endef

#DEPENDENCY FOR SERVER
define add_test_server_dependency_wakaama =
	echo 'include $(RIOTBASE)/Makefile.base' > $(PKG_BUILDDIR)/examples/server/Makefile;
	"$(MAKE)" -C $(PKG_BUILDDIR)/examples/server
endef

#DEPENDENCY FOR BOOTSTRAP_SERVER
define add_test_bootstrap_server_dependency_wakaama =
	echo 'MODULE:=test_bootstrap_server' > $(PKG_BUILDDIR)/core/Makefile;
	echo 'include $(RIOTBASE)/Makefile.base' >> $(PKG_BUILDDIR)/examples/bootstrap_server/Makefile;
	"$(MAKE)" -C $(PKG_BUILDDIR)/examples/bootstrap_server
endef

#DEPENDENCY FOR EXAMPLES
define add_shared_dependency_wakaama =
	echo 'MODULE:=shared_wakaama' > $(PKG_BUILDDIR)/examples/shared/Makefile;
	echo 'include $(RIOTBASE)/Makefile.base' >> $(PKG_BUILDDIR)/examples/shared/Makefile;
	"$(MAKE)" -C $(PKG_BUILDDIR)/examples/shared
endef

#BASE MAKEFILE FOR WAKAAMA
define add_base_makefile_wakaama =
	echo 'MODULE:=wakaama' > $(PKG_BUILDDIR)/core/Makefile;
	echo 'CFLAGS += -I$(PKG_BUILDDIR)/core/er-coap-13' >> $(PKG_BUILDDIR)/core/Makefile;
	echo 'include $(RIOTBASE)/Makefile.base' >> $(PKG_BUILDDIR)/core/Makefile;
	"$(MAKE)" -C $(PKG_BUILDDIR)/core
endef

include $(RIOTBASE)/pkg/pkg.mk
