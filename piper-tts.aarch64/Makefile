BINS = \
	piper \
	piper_phonemize \
	espeak-ng

LIBS = \
	libespeak-ng.so.1 \
	libonnxruntime.so.1.14.1 \
	libpiper_phonemize.so.1 \
	libtashkeel_model.ort

prefix ?= /usr
bindir ?= $(prefix)/bin
libdir ?= /lib/aarch64-linux-gnu

BINS_EXP = $(patsubst %, $(DESTDIR)$(bindir)/%, $(BINS))
LIBS_EXP = $(patsubst %, $(DESTDIR)$(libdir)/%, $(LIBS))

.PHONY: install
install:	$(BINS_EXP) $(LIBS_EXP) 

$(DESTDIR)$(bindir)/piper:	piper
	install -D -m 0755 $< $@

$(DESTDIR)$(bindir)/piper_phonemize:	piper_phonemize
	install -D -m 0755 $< $@

$(DESTDIR)$(bindir)/espeak-ng:	espeak-ng
	install -D -m 0755 $< $@

$(DESTDIR)$(libdir)/libespeak-ng.so.1:	libespeak-ng.so.1.52.0.1
	install -D -m 0644 $< $@

$(DESTDIR)$(libdir)/libpiper_phonemize.so.1:	libpiper_phonemize.so.1.2.0
	install -D -m 0644 $< $@

$(DESTDIR)$(libdir)/libonnxruntime.so:	libonnxruntime.so.1.14.1
	install -D -m 0644 $< $@

$(DESTDIR)$(libdir)/%:	%
	install -D -m 0644 $< $@
