ACLOCAL_AMFLAGS = -I m4 ${ACLOCAL_FLAGS}

SUBDIRS = \
	babl		\
	extensions	\
	tools		\
	tests

if ENABLE_DOCS
SUBDIRS+= docs
endif

pkgconfigdir = $(libdir)/pkgconfig
pkgconfig_DATA = babl.pc

built_dist_files = README

EXTRA_DIST = \
	$(built_dist_files)	\
	AUTHORS			\
	COPYING			\
	INSTALL			\
	NEWS			\
	TODO			\
	autogen.sh		\
	babl.pc.in		\
	export-symbols

DISTCLEANFILES = \
	$(built_dist_files)	\
	babl.pc

.PHONY: snapshot


if HAVE_W3M
README: all docs/index.html
	$(W3M) -cols 72 -dump docs/index.html > $@
else
README:
	@echo "*** w3m must be available in order to make dist"
	@false
endif

snapshot:
	$(MAKE) dist distdir=$(PACKAGE)-`date +"%Y%m%d"`
snapcheck:
	$(MAKE) distcheck distdir=$(PACKAGE)-`date +"%Y%m%d"`

distclean-local:
	if test $(srcdir) = .; then :; else 	\
		rm -f $(BUILT_EXTRA_DIST);	\
	fi

.PHONY: list
list:
	@$(MAKE) -pRrq -f $(lastword $(MAKEFILE_LIST)) : 2>/dev/null | \
	awk -v RS= -F: \
	'/^# File/,/^# Finished Make data base/ {if ($$1 !~ "^[#.]") {print $$1}}' \
	| sort | egrep -v -e '^[^[:alnum:]]' -e '^$@$$' | xargs
