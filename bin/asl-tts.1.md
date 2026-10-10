% asl-tts(1) ASL3 2024
% Jason McCormick
% August 2024

# NAME

asl-tts - ASL text to speech for Asterisk/app\_rpt

# SYNOPSIS

usage: `asl-tts -n NODE -t "TEXT" [ -v VOICE ] [ -f FILE ] [ -cp ]`

# DESCRIPTION

asl-tts uses the piper-tts text to speech engine to generate
ulaw files from text so that Asterisk/apt\_rpt can speak any set of
arbitrary text without needing to have a sound file installed for the
word necessary.

By default, asl-tts will cause app\_rpt to immediately speak whatever
text was specified. To create the text for other usage, such as cron
jobs, use the "-f FILE" option to specify where the file should be
created. Do not use an extension; the file will be automatically appended
with the .ul postfix.

Running the piper-tts system takes a few seconds to compile the voice into
the sound file. Larger text blocks may take tens of seconds to compile.

Note that temporary files are written to /tmp/asl-tts-${USER}/ and are not
automatically cleaned up because it's impossible to know when
Asterisk will actually need/speak the file contents. If this becomes
a problem, put in a systemd timer unit or a cron job to delete old
files in /tmp/asl-tts-${USER}. For example, calling `asl-tts` as root, the
files will be in `/tmp/asl-tts-root`; called as asterisk, the files
will be in `/tmp/asl-tts-asterisk`.

# VOICES

By default, the package provides on voice "Amy" from
https://github.com/rhasspy/piper/blob/master/VOICES.md. It is possible
to download other voices, for any language, and store the .onnx and
.onxx.json file in /var/lib/piper-tts and then use them with the -v option.
For example, to add the English en\_GB voice alan from the voices repository:

1. Download the .onnx and .onnx.json file to /var/lib/piper-tts

2. Specify "-v en\_GB-alan-low.onnx" on the command line
to asl-tts.

Note, since all files are squashed down to 8K uLaw format, there is no value
in the "medium" or "high" quality models. Always use the low quality model.

# OPTIONS

* **-n NODE**: The node to play on (required)
* **-t "TEXT"**: The text to speak (required)
* **-v VOICE**: The voice .onnx file relative to /var/lib/piper-tts (optional)
* **-f FILE**: Write out the text to a file rather than play (optional)
* **-c**: Sleep to the length of the file and then delete the
     files. Note that this is undesirable for long files or cron jobs
     and cleanup should be done separately. (optional)
* **p**: Use `rpt playback` rather than `rpt localplay` for the speech (optional)

# EXAMPLE

`asl-tts -n 1999 -t "Good morning"` will speak "Good morning" over
the system.

More complex message can be created with additional shell coding. As an
example here's how the current public IP address of the system could be
obtained and spoken:

```bash
IPADDR=$(wget -q -O - checkip.dyndns.com | grep -Po "[\d\.]+")
MSG="The time is ${IPADDR}"
asl-tts -n 1999 -t ${MSG}
```

# BUGS

Report bugs to https://github.com/AllStarLink/asl3-tts/issues

# COPYRIGHT

Copyright (C) 2024-2026 Jason McCormick and AllStarLink
under the terms of the MIT License.
