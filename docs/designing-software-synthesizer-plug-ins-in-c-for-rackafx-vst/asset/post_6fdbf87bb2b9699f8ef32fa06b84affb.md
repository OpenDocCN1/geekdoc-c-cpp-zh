
```
min:MIN_NOISE_OSC_AMP_DB
max:MAX_NOISE_OSC_AMP_DB
def:DEFAULT_NOISE_OSC_AMP_DB
oltOctave:no
integerControl:NO;
```

```
[controlArray addObject:wpRotaryKnob_0];
[wpRotaryKnob_0 setKnobImageArray:knobImages];
```

```
[wpRotaryKnob_1 initControlWithName:@"Pulse Width*"
controlIndex:PULSE_WIDTH_PCT
min:MIN_PULSE_WIDTH_PCT
max:MAX_PULSE_WIDTH_PCT
def:DEFAULT_PULSE_WIDTH_PCT
```

```
voltOctave:no
integerControl:NO;
```

```
[controlArray addObject:wpRotaryKnob_1];
[wpRotaryKnob_1 setKnobImageArray:knobImages];
etc...
```

```
[wpOMG_0 initControlWithName:@"LFO Waveform*"
controlIndex:LFO_WAVEFORM
enumString:"sine,usaw,dsaw,tri,square,expo,rsh,qrsh"
def:DEFAULT_LFO_WAVEFORM
```

```
VerySmallFont:NO;
```

```
[controlArray addObject:wpRotaryKnob_03];
etc...
```

```
[wpRotaryKnob_27 initControlWithName:@"PBRange*"
controlIndex:PITCHBEND_RANGE
min:MIN_PITCHBEND_RANGE
max:MAX_PITCHBEND_RANGE
def:DEFAULT_PITCHBEND_RANGE
```

```
voltOctave:no
integerControl:YES;
```

```
[controlArray addObject:wpRotaryKnob_27];
[wpRotaryKnob_27 setKnobImageArray:knobImages];
```

-- parse background image

```
NSString* path = [[NSBundle bundleForClass:[MiniSynthView class]] pathResource:@"medgrey-Brushed" ofType:@"bmp"] autorelease];
```

```
backImage = [[NSImage alloc] initWithContentsWithPath:path];
```

```
[NSURL URLWithPath:path];
```

- (void)dealloc
{
    [self removeListeners];
    [backImage release];
    [backgroundColor release];
    [controlArray dealloc];
    [knobImages dealloc];
    [super dealloc];
}

- (void)drawRect:(NSRect)rect

// --- make the tiled background pattern as a UIColor
NSColor *backgroundPattern = [NSColor colorWithPatternImage:backImage];

// --- fill it
[backgroundPattern setFill];
NSRectFill(rect);

// --- do group frame background images
float x, y, w, h;
float y0Offset = -7;

// --- column 1
//
// --- bottom knob
NSRect knob3Rect = [wpRotaryKnob_3 frame];
x = NSMinX(knob3Rect);
w = NSWidth(knob3Rect);

// --- top knob
NSRect knob0Rect = [wpRotaryKnob_0 frame];
y = NSMinY(knob0Rect);

// --- height of col
h = y + NSHeight(knob0Rect) + 50;

// --- group frame
NSRect rect1 = [NSMakeRect(x, y0Offset, w, h)];

// --- get the image
NSString* path = [[[NSBundle bundleForClass:[MiniSynthView class]] pathForResource:@"groupframe" ofType:@"png"] autorelease];

NSImage* image = [[NSImage alloc] initWithContentsOfURL:[NSUrl fileURLWithPath:path]];

float alpha = 1.0;

// --- paint it
if(image) {
    [image drawInRect:groupRect1 fromRect:NSZeroRect
    operation:NSCompositesSourceover fraction:alpha];

    // --- column 2
    etc...

    // --- we call super to draw all other controls after we have filled
    // background
    [super drawRect:rect];
}

# Chapter 3: MIDI

In this chapter we will start a synth project called NanoSynth. This is going to be an important project because we are going to use it to build up a synth architecture that will be used in all the rest of the projects. Additionally, when you design the C++ objects that will become the synth guts in Chapters 4 – you will test them in NanoSynth. The MIDI message decoding we set up in NanoSynth will be used throughout the rest of the book. To save space, it won't be repeated for every project, even if you know MIDI, it is still important to understand how NanoSynth works.

## 3.1 MIDI Messages

MIDI is a messaging system. There is a sender and a receiver for each message. The messages are designed to codify as much information as possible in the shortest message possible. The messages also need to convey vastly different types of information. Some messages require extra data to fully transmit the information. The MIDI inventors first broke down the types of messages their synthesizers would need to send and receive. They implemented a system to handle future messages and data that would likely be invented as time progressed. Figure 3.1 shows the different kinds of MIDI messages in the specification. The Voice Message where you will spend the majority of your time in the book. The Channel Messages have a particular destination on a device whereas System Messages are global and are broadcast to all devices. The rest of the messages are as follows:

**Channel:**
- Voice: performance information and note events
- Channel Mode: configuration changes

**System:**
- System Common: information for all devices
- System Real Time: timing (clock)
- System Exclusive: anything and everything (open ended)

The synth projects in this book only deal with Channel messages, the most common and certainly important. These not only include note messages, but all the Continuous Messages (CCs) for knobs and sliders. MIDI messages are transmitted serially by bytes. Figure 3.2 shows the structure of a MIDI byte. MIDI bytes encode types of information: status—the kind of message being sent and data—information about the message. The status/data bit is the Significant Bit (MSB), which is the leftmost bit of a MIDI byte. The status byte is broken into four nibbles. The lower nibble encodes the channel 0–15. The upper nibble is the message whose upper bit is always 1. For data bytes, the lower seven bits encode the data. This provides 128 different values from 0 to 127. A MIDI message consists of at least one status byte and zero or more data bytes. The status byte is always the first in the message. It determines the number of data bytes that will follow. This way, the receiving device knows how to interpret future data bytes.

![](img/b42d0ca53f4a88d55f7cc5d174_0.png)
Figure 3.1: The MIDI Message hierarchy.

![](img/b42d0ca53f4a88d55f7cc5d174_1.png)
Figure 3.2: The MIDI byte uses status/data MSB to identify the type of message component.

## 3.2 Channel Voice Messages

The Channel Voice messages contain most important information that we need. These are listed in Table 3.1. Let's examine each message.

### 0x8n—Note Off

The note off message encodes the MIDI note number and the velocity with which the key was released, most keyboards do not offer this release-velocity option. The note number and velocity are interpreted the same way as for note messages below. Interestingly you can transmit a note off message by sending a note on message with velocity of 0. This is common because it is part of another scheme which is a way of compressing data when the status bytes are the same.

### 09n-Note On

The note on message encodes the MIDI note number and the velocity with which the key was struck. For controllers that do not respond to velocity such as vintage synths or inexpensive USB controllers, a value of 64 is often transmitted. There are 128 MIDI notes, indexed from 0 to 127. The MIDI 1.0 spec places middle C at note number 60 and the entire set of notes spans the range of 128 semitones (or 12800 cents) or frequencies from note0 (a C at ~8.18 Hz) to 127 (a G at ~12.5 kHz).

Table 3.1: MIDI messages.

| byte n = channel | Message | Data Byte 1 | Data Byte 2 |
|---|---|---|---|
| 1000n = 08n | Note Off | MIDI Note # | Velocity |
| 1001n = 09n | Note On | MIDI Note # | Velocity |
| 1010n = 0An | Aftertouch | MIDI Note # | Pressure |
| 1011n = 0Bn | Control Change | Type | Value |
| 1100n = 0Cn | Program Change | Program # | ---- |
| 1101n = 0Dn | Channel Pressure | Pressure | ---- |
| 1110n = 0En | Pitch Bend | LSB | MSB |
| 1111n = 0Fn | unused | unused | unused |

Velocity is specified as follows: 0 is silence, 1 is ppp, 64 is between mp and mf. Using the musical conventions, pp is pianissimo, and mf are mezzo-piano and mezzo-forte, and ff is fortissimo. Several schemes exist for converting the velocity value 0–127 into this musical loudness range, which is essentially exponential in nature. We will use the MMA's convex transform for this when time comes for implementation, but you are encouraged to seek out and try different mapping schemes.

### 0An—Aftertouch

Some keyboards can sense pressure after the key has been struck and has bottomed out. You strike the key and then press down after the note sounds. Sensing components convert that pressure into a voltage that is converted into a pressure value. If the keyboard can do this for individual notes—that is, sense different pressures on different keys that have been pressed—then it supports Aftertouch (also known as Key Aftertouch, Polyphonic Key Pressure, and Polyphonic Aftertouch).

### 0Bn—Control Change

Most MIDI controllers feature an abundance of assignable controller knobs, sliders, ribbons and switches, in addition to a pitch bend control (ystick or wheel) and a modulation control (usually a wheel or slider labeled Mod or Modulation). All of these controls, including sustain and sostenuto pedals, are Continuous Controllers. There are 128 continuous controllers indexed from 0 to 127. The MIDI spec only implements some of them; many are designated as "Undefined." All of our synths are responding to a core set of CCs. These are shown in Table 3.2.

Table 3.2: Control Change messages that all your synths will support.
