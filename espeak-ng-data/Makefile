ESPEAK = $(filter-out Makefile, $(shell find . -type f | sed 's/\.\///g'))

prefix ?= /usr
share_prefix ?= $(prefix)/share/espeak-ng-data

ESPEAK_EXP = $(patsubst %, $(DESTDIR)$(share_prefix)/%, $(ESPEAK))

.PHONY: install
install:	$(ESPEAK_EXP)

$(DESTDIR)$(share_prefix)/%:	%
	install -D -m 0644 "$<" "$@"
