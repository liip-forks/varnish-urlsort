INCLUDES = -I$(VARNISHSRC)/include -I$(VARNISHSRC)

vmoddir = $(VMODDIR)
vmod_LTLIBRARIES = libvmod_urlsort.la

libvmod_urlsort_la_LDFLAGS = -module -export-dynamic -avoid-version

libvmod_urlsort_la_SOURCES = \
	vcc_if.c \
	vcc_if.h \
	vmod_urlsort.c

vcc_if.c vcc_if.h: $(VARNISHSRC)/lib/libvmod_std/vmod.py $(top_srcdir)/src/vmod_urlsort.vcc
	@PYTHON@ $(VARNISHSRC)/lib/libvmod_std/vmod.py $(top_srcdir)/src/vmod_urlsort.vcc

VMOD_TESTS = tests/*.vtc
.PHONY: $(VMOD_TESTS)

tests/*.vtc:
	$(VARNISHSRC)/bin/varnishtest/varnishtest -Dvarnishd=$(VARNISHSRC)/bin/varnishd/varnishd -Dvmod_topbuild=$(abs_top_builddir) $@

check: $(VMOD_TESTS)

EXTRA_DIST = \
	vmod_urlsort.vcc \
	$(VMOD_TESTS)

CLEANFILES = $(builddir)/vcc_if.c $(builddir)/vcc_if.h
