
The key object for most simple applications is uBit.audio.soundExpressions and the most commonly used methods are play("sound") and playAsync("sound") which do the same job, playAsync runs in the background. The sound string can be used to specify the sound you want in detail there are some predefined sounds available:

| giggle | hello | sad | soaring | twinkle |
| happy | mysterious | slide | spring | yawn |

It has to be said that many of the sound effects don't sound much as described!
The sounds produced are described by a fairly complicated string format with 72 characters per audio sample:

Start
[0] wave 0 SineTone
1 SawtoothTone
2 TriangleTone
3 SquareWaveTone
4 Noise

```
[1] volume 0000-1023
[5] frequency 0000-9999
[9] duration 0000-9999
[13] shape 00 noInterpolation
01 linearInterpolation
02 curveInterpolation
05 exponentialFallingInterpolation;
06 exponentialFallingInterpolation;
08 aggrioAscending majorScale
09 aggrioDescending majorScale
10 aggrioAscending minorScale
11 aggrioDescending minorScale
12 aggrioAsc diminished
13 aggrioDescending diminished
14 aggrioAscending chromatic
15 aggrioDescending chromatic
16 aggrioAscending wholeTone
17 aggrioDescending wholeTone
18 logarithmicInterpolation;
```

[15] unused XXX
[18] end frequency 0000-9999
[22] unused XXX
[26] end volume 0000-1023
[30] steps 0000-9999
[34] fx choice 00 volumeRampEffect
01 frequencyVibratoEffect
02 volumeVibratoEffect
03 warbleInterpolation

[36] fxParam 0000-9999
[40] fxnSteps 0000-9999

[44] freq. random 0000-9999
[48] end freq 0000-9999
[52] volume random 0000-9999
[56] end vol random 0000-9999
[60] duration random 0000-9999
[64] fxParamRandom 0000-9999
[68] fxnStepsRandom 0000-9999

The duration is set approximately in milliseconds and the frequency is approximately in Hertz. The basic idea is that you set a start and end frequency and volume and then choose how these change over the duration. So selecting linear interpolation makes the frequency and volume change smoothly from start to end values. There are lots of other ways that you can modify the sound by applying effects and random changed, but this is beyond the scope of this book.

If we write a short function which can change any part of a ManagedString then it is easier to construct an audio effect:

```
ManagedString setSound(ManagedString audio,
    ManagedString data, int s)
{
    return audio.substring(0, s) + data +
        audio.substring(s + data.length(),
        audio.length() - s data.length());
}
```

Using this we can create a simple effect that plays a constant sine wave for 500ms:

```
#include "MicroBit.h"
MicroBit uBit;
int main() {
	uBit.initString();
	// 72 characters
	static ManagedString soundData(
		"0000000000000000000000000000000000000000000000000000000000");

soundData = setSound(soundData, "0", 0); // Wave
soundData = setSound(soundData, "1023", 1); // volume start
soundData = setSound(soundData, "1023", 26); // volume end
soundData = setSound(soundData, "1000", 5); // frequency start
soundData = setSound(soundData, "1000", 18); // frequency end
soundData = setSound(soundData, "0", 13); // shape

soundData = setSound(soundData, "500", 9); // duration
soundData = setSound(soundData, "0128", 30); // steps

uBit.audio.soundExpressions.play(soundData);

	return 0;
}
```

This just makes a beep as intended.
If you change the specification to:

```
soundData = setSound(soundData, "01", 13); // shape
soundData = setSound(soundData, "9000", 18); // frequency end
```

You will hear a rising tone.
It is worth saying the sound effects involve more than one frame of 72 characters to create a set of audio changes.
If this all seems too much to create a simple beep, then the good news is that the approach in the microbit V1 also works when redirected to the speaker pin:

```
void analogPitch(int frequency, int vol, int ms) {
	uBit.io.speaker.setAnalogValue(vol);
	uBit.io.speaker.setAnalogPeriodUs(1000000/frequency);
	uBit.io.sleep(ms);
	uBit.io.speaker.setAnalogValue(0);
}
```

# Morse Code Transmitter

As a slightly more sophisticated example using the radio and sound, let's implement a Morse code transmitter. Morse code is old-fashioned but still relevant and it is worth knowing. The idea is that each letter of the alphabet is coded as a sequence of short and long tones usually called a dot and a dash, for example, the letter A is dot dash. The key idea is that there is no set length of time for a dot or a dash except that a dash should be three times longer than a dot and letters are separated by a dot length of silence.

Creating a Morse code transmission program is just a matter of setting an LED off and starting a sound when Button A is pressed and turning the LED off and stopping the sound when it is released. The simplest way to do this is to make use of the button down and up. The simplest way to do this is to make use of the button down and up. If we use the radio to to call the appropriate functions. This makes the program on the local microbit.

```
#include "MicroBit.h"
MicroBit uBit;

void beepOn(ManagedString e) {
    // ...
}

void beepOff(ManagedString e) {
    // ...
}
```
(Note: The OCR for the Morse code functions was fragmented in the source; the logic has been cleaned/reconstructed based on the provided snippets.)
