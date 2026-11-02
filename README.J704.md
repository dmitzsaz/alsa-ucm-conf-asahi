# J704 audio profiles

MacBook Pro 14-inch with the base M5 SoC (J704) exposes two macaudio cards:

| Card long name | ALSA ID | Playback |
| --- | --- | --- |
| MacBook Pro J704 | AppleJ704 | Six speakers on PCM 1 |
| MacBook Pro J704 Jack | AppleJack | Stereo headphones on PCM 0 |

The speaker card uses the shared speaker-only laptop verb. It selects the
Secondary playback mux, enables the speaker switch and exposes six channels
in order LW1, RW1, LW2, RW2, LT, RT. The jack profile uses the headphone jack
switch and hardware DAC volume. It intentionally describes playback only;
headset capture is not added by this change.

The separate `MacBook Pro J704 AOP Audio` card (`AppleJ704AOP`) exposes its
three-microphone array on PCM 1. Its profile uses three capture channels and
the Internal Mic Jack control, which follows the hardware disconnect when
the lid closes. Use the matching asahi-audio microphone filter to turn the
raw array into the mono MacBook Pro Microphone source. Low-power microphone
capture is not a user route on J704.

Use these profiles with the J704 AOP/macaudio support in the kernel, the J704
asahi-audio DSP and speakersafetyd's J704 profile. Speaker routing alone does
not provide EQ or thermal protection. The card names are the names in the
published J704 device tree; old jack-only bring-up trees using the speaker
card's long name are not supported by this profile.
