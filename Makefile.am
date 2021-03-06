
ACLOCAL_AMFLAGS = -I config

include $(top_srcdir)/config/rpm.am
include $(top_srcdir)/config/deb.am
include $(top_srcdir)/config/tgz.am

SUBDIRS = include rpm
if CONFIG_USER
SUBDIRS += lib cmd man scripts
endif
if CONFIG_KERNEL
SUBDIRS += module

extradir = /usr/src/spl-$(VERSION)
extra_HEADERS = spl.release.in spl_config.h.in

kerneldir = /usr/src/spl-$(VERSION)/$(LINUX_VERSION)
nodist_kernel_HEADERS = spl.release spl_config.h module/$(LINUX_SYMBOLS)
endif

AUTOMAKE_OPTIONS = foreign
EXTRA_DIST  = autogen.sh META DISCLAIMER copy-builtin
EXTRA_DIST += config/config.awk config/rpm.am config/deb.am config/tgz.am

distclean-local::
	-$(RM) -R autom4te*.cache
	-find . \( -name SCCS -o -name BitKeeper -o -name .svn -o -name CVS \
		-o -name .pc -o -name .hg -o -name .git \) -prune -o \
		\( -name '*.orig' -o -name '*.rej' -o -name '*~' \
		-o -name '*.bak' -o -name '#*#' -o -name '.*.orig' \
		-o -name '.*.rej' -o -name 'aclocal.m4' -o -size 0 \
		-o -name '*%' -o -name '.*.cmd' -o -name 'core' \
		-o -name 'Makefile' -o -name '$(LINUX_SYMBOLS)' \
		-o -name '*.order' -o -name '*.markers' \) \
		-type f -print | xargs $(RM)

dist-hook:
	sed -i 's/Release:[[:print:]]*/Release:      $(RELEASE)/' \
		$(distdir)/META

ctags:
	$(RM) $(top_srcdir)/tags
	find $(top_srcdir) -name .git -prune -o -name '*.[hc]' | xargs ctags

etags:
	$(RM) $(top_srcdir)/TAGS
	find $(top_srcdir) -name .pc -prune -o -name '*.[hc]' | xargs etags -a

tags: ctags etags

pkg: @DEFAULT_PACKAGE@
pkg-kmod: @DEFAULT_PACKAGE@-kmod
pkg-utils: @DEFAULT_PACKAGE@-utils
