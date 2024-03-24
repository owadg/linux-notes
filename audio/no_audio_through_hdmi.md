# No Audio Through HDMI
---
## Situation
I was bumbling along and updated my stuff. I restarted my PC after, and when I did, I had no audio. When I went to look for the device using the KDE System Audio GUI. It showed up as a disabled device.

## Research
I learned about pipewire, pulseaudio, and ALSA. I have pipewire installed. The KDE GUI program uses pulseaudio, which led me to believe that most of my audio was through the pulseaudio API provided by pipewire. I found my monitor output as a playback device in ALSA by using the following command:
`$ aplay -l`
I found which one it was by tring to use ALSA to play a .wav file. The command is:
`aplay -D plughw:[card number here],[device number here] [wav file location]`
After, I went and looked through my pipewire configuration by using the following commands:
`$ pactl list cards`
and
`$ pactl list sinks`
I found out that for some reason, all the profiles I had did not include the device I found in ALSA. I added it by using the following command:
`$ pactl load-module module-alsa-sink device=hw:[card number here], [device number here]`
I didn't edit the config file so I am sure I will have to do that.
If I have to do that I can just use this documentation to add it to the pipewire pulse config.
https://docs.pipewire.org/page_pulse_modules.html
