VOICES = \
	en_US-amy-low.onnx \
	en_US-amy-low.onnx.json

prefix ?= /usr
voice_prefix ?= $(prefix)/lib/piper-tts/voices
voice_link_prefix ?= /var/lib/piper-tts

VOICES_EXP = $(patsubst %, $(DESTDIR)$(voice_prefix)/%, $(VOICES))

.PHONY: install
install:	$(VOICES_EXP)

$(DESTDIR)$(voice_prefix)/%:	%
	install -D -m 0644 $< $@
	test -d $(DESTDIR)$(voice_link_prefix) || mkdir -p $(DESTDIR)$(voice_link_prefix)
	ln -sf $@ $(DESTDIR)$(voice_link_prefix)/$<
