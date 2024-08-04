VOICES = \
	en_US-amy-low.onnx \
	en_US-amy-low.onnx.json

prefix ?= /usr
voice_prefix ?= $(prefix)/lib/piper-tts/voices

VOICES_EXP = $(patsubst %, $(DESTDIR)$(voice_prefix)/%, $(VOICES))

.PHONY: install
install:	$(VOICES_EXP)

$(DESTDIR)$(voice_prefix)/%:	%
	install -D -m 0644 $< $@
