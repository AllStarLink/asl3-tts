prefix ?= /usr
bindir ?= $(prefix)/bin
mandir ?= $(prefix)/share/man

BINS = $(filter-out Makefile $(wildcard *.1.md), $(wildcard *))
BIN_INSTALLABLES = $(patsubst %, $(DESTDIR)$(bindir)/%, $(BINS))

MANS = $(wildcard *.1.md)
MAN_INSTALLABLES = $(patsubst %.md, $(DESTDIR)$(mandir)/man1/%, $(MANS))

install:	$(BIN_INSTALLABLES) $(MAN_INSTALLABLES)

$(DESTDIR)$(bindir)/%: %
	install -D -m 0755  $< $@

$(DESTDIR)$(mandir)/man1/%: %.md
	mkdir -p $(DESTDIR)$(mandir)/man1
	pandoc $< -s -t man > $@
