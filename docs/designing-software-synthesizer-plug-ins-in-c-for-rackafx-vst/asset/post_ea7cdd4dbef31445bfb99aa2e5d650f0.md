
Chapter 9 is a turning point in the book because all of the underlying synthesizer C++ objects are set in code and will not change. Here you design MiniSynth, the Analog Modeling synthesizer. You can deviate from the book, implementing your own synth voice objects and your model coding if you wish. In Chapter 10, you learn how to use audio files to import DigiSynth, a stereo playback synthesizer. Chapter 11 on Vector Synthesis uses the sample-based oscillators in the Vector project and includes a bonus project AniSynth, which is an interpretation of the Moog Anisynthhesizer Android app. In Chapter 12, you design a clone of the Yamaha DX100 FM synthesizer. Chapter 13 is the audio effects chapter that shows you how to add a delay of effects to MiniSynth, in which you greatly extend your synth capabilities. Brief Appendix shows you how to convert your VST and AU Template into the base code for your project (this isn't needed by RackAFX if it creates your project for you).

There are two people who greatly influenced the book early—Bill Jenkins and Andy Lear, both Senior Engineers at K Research and Development, who were reviewers of the original proposal. Bill's comments and suggestions shaped the way the C++ code is presented and interleaved as much as possible with descriptive text. In fact, his is the reason that the different API is coded in separate sections rather than mixed together as is in the proposal. There is no word in the English language that describes gratitude for Andy's input on the theory chapters (4–8). He is an expert on many of the algorithms in these chapters having his input was invaluable. Andy also proofread chapters repeatedly, offering a continuous stream of ideas. The analog MiniSynth sounds fantastic to me, and much of this is due to Andy's input. Bill and Andy—thank you!

My fellow professors and students were also enthusiastic about the effort and I received full support from my colleagues Dean Shelby, Serona Elton, Rey Sanchez, Colby Leider, Joe Abbatti and Chris Bennett, including some needed leeway in my poor attendance record in Music Engineering Forum class. Although I began teaching synth classes in the 1990s, it was only four years ago that the students started using RackAFX. The last few generations of Music Engineering students have also shaped the content of the book and RackAFX software, whether they know it or not. Last year, Colin Franks and Mark Gill improved the stability and performance of several synth components. Rob Reinh revamped GUI elements. I also need to thank the students for their input and help in last year's synth class (alphabetically): Daniel Avissar, Andy Ayers, Daniel Bennett, Garrett Claussen, Sammy Falcon, Michael Intenda, Connor McCullough, Tac Nicol, Crispin Odomn, Andrew O'Neil-Smith, Ross Penniman, Michael Tony and Francisco Valencia Otalvar.

You can stay in touch with me by joining the Forum at my website http://www.willpirkle.com/synth/, which also contains information and resources that are not included in the book. As usual, I encourage you to send me your creations or post links to the forum. As my last book, I can't wait to hear what you cook up in plug-in development!

All the best,
Will Pirkle
June 1, 2014

# Foreword

Here are some notes about the book projects, and conventions.

# Skills

Basic C++ programming skills are all written in C++. If you have taken a university class or two on the subject, you should have no problem. In APIs, you need to be fully competent with the Visual Studio compiler, and you need to know how to add files to your projects, use filters to rearrange the source files, and use the debugger. If you want to design a GUI, you need to be competent with frameworks like AppKit and CoreAudio; likewise you need to know InterfaceBuilder and Xcode.

# Hungarian Notation

99% of RackAFX and VST code is written using Hungarian notation. Much of the AU code uses it as well (some from Apple, Inc.). Here is Microsoft's description of Hungarian notation: Long ago in the early days of DOS, Microsoft's Chief Architect Charles Simonyi introduced a naming convention that adds a prefix to the identifier name to indicate its functional type. This system became widely known inside Microsoft as "Hungarian notation" because prefixes make variable names look a bit like they are written in non-English language. Turns out, Hungarian naming is quite useful—one technique among many that helps programmers produce better code. Since most headers and documentation published over the last 15 years have used Hungarian notation for identifiers, the most important publication was the first read by almost every Windows programmer (Simonyi, 1999).

# Synth Projects

During the course of the book, you develop six projects from any of the APIs. The code is split into sections for each API. The chapters follow the same sequence of presentation of ideas then you can read the first theory, then skip ahead to the section that contains your target platform. The projects are designed so that you may spin off many variations of your own. Here is a list of the synth projects and the components they contain:

| Project | Oscillators | Filters | | | |
| :--- | :--- | :--- | :--- | :--- |
| NanoSynth | analog modeling (BLEP) | Moog Ladder | general purpose LFO | combination Amp-EG, Filter-EG, Pitch-EG |
| MiniSynth | analog modeling (BLEP) | Moog Ladder | general purpose LFO | combination Amp-EG, Filter-EG, Pitch-EG |
| DigiSynth | sample-playback | Oberheim SEMF | general purpose LFO | combination Amp-EG, Filter-EG, Pitch-EG |
| VectorSynth | sample-playback | Korg Lowpass | general purpose LFO | combination Amp-EG, Filter-EG, Pitch-EG |
| AniSynth | sample-playback | Diode Ladder | general purpose LFO | combination Amp-EG, Filter-EG, Pitch-EG |
| DxSynth | wavetable | None | general purpose LFO | FM EGs |

# Delay FX

The suite of delay effects in Chapter 13 is added to MiniSynth as an example, but it may just easily be added to any of the synths, you are encouraged to implement FX in all synths.

# Bibliography

Simonyi, Charles. 1999. "Hungarian Notation." Accessed August 2014. http://msdn.microsoft.com/en-us/library/aa26976vs.aspx

# Chapter 1: Synthesizer Fundamentals

The synthesizer is usually defined vaguely as an electronic instrument that produces and controls sounds. When discussing this with our colleagues, we agreed that the density of this definition might be constraining. Why couldn't the didgeridoo or the Jew's harp be considered synthesizers? In fact, might no other than the human voice be a synthesizer? Consider the American inventor Thaddeus Cahill to be the inventor of the modern synthesizer. In 1897, he applied for a patent for the Telharmonium or Dynaphone, an instrument that used steam power electric generators to synthesize sinusoids—it was even polyphonic (capable of playing more than one note at a time). Leon Ther invented the Theremin in 1919, which included a touchless interface that controlled the amplitude and pitch of a sinusoid. Unlike the Telharmonium, the Theremin used electronic amplifiers to reproduce the sound rather than acoustic horns. However, inventors created unique instruments like the Ondes Marten, Trautonium, and Mixtartonium, to name a few. The first use of the word synthesizer is in the Complexplex Synthesizer of 1929. RCA marked the Electronic Music Synthesizer that used tuning forks to control the oscillations. Max Mathews experimented with computers for rendering and controlling an audio signal in 1957, while Robert Moog popularized the hardware and is credited with inventing the first voltage-controlled synth in 1963. His inventions include the Moog ladder, which we will study in Chapter 7. In 1967, he marketed electronic modules that could be connected in systems to produce various sounds—he called these synthesizers. The driving force for these synthesizers was not electronic music but rather neoclassical composers of the 20th century. It is not uncommon to read about associations between composers and electronic engineers, for example Moog worked with composer Herbert Deutsch and Donald Buchla teamed up with composers Morton Subotnik and Ramon Sender to produce avant-garde compositions. Sergio Franco and Ken Pohlmann worked with composer Salvatore Martini and the SAL-MAR construction shown in Figure 1.1 in the 1970s.

Moog's synthesizers consist of various components, each with its own board, knobs, lights, and joints. The oscillator generates primitive waveforms—sinusoid, sawtooth, and square. The amplifier uses a voltage-controlled amplifier to modify the amplitude of a signal. The filter implements various basic functions such as low-pass and high-pass types. The envelope generator creates a varying output value that is used to control the amplitude or filtering of other modules. Combining the modules in various ways produces the most interesting sounds; the result is somehow greater than some of the parts. Each of Moog's modules had its own output, and control jacks were connected together using audio patch cables, which were adopted widely use across record studios. This is the origin of the term patch, which we use often. A patch is a recipe for connecting and setting up the parameters of each module to form a specific sound. You hear the term patch cord patch patch all the time when around synthesizers.
