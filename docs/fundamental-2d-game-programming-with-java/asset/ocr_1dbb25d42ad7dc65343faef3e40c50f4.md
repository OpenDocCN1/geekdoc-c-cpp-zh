# WORKING WITH SOUND FILES

The sound API only handles a few file formats: *.wav, *.aiff, and *.au. Other more popular formats are not supported without third-party software.

A sound file has a number of attributes that are important. Each file contains a number of samples. Each sample, or frame, is the sound at that specific point in time. Sound files have a frame rate, or sample rate, measured in hertz. For example, a sample rate of 44,100Hz has 44,100 samples per second. Another important attribute is bits-per-sample. An 8-bit sound file stores the frame as eight bits of data, or one byte, whereas a 16-bit sound file stores the sound as two bytes. The number of channels is also important. There is one sample of data for each channel in every frame. That means that a 16-bit sound with two channels (stereo) has 16 bits + 16 bits, or 32 bits of data per frame.

frame size in bytes =
bits per frame
8
* number of channels

The format of the sound data and calculating the number of bytes for each frame is important later, when buffer sizes for streaming data need to be created. For now, just be aware that all these attributes will change for every different type of sound file.

To play an audio file, you need an AudioInputStream. The problem with these stream objects is, like most InputStream objects, they can only be used once. In order to use sounds over and over for a game, the raw sound bytes need to be extracted from the file. They can then be wrapped in a ByteArrayInputStream and used to create an AudioInputStream without streaming the data from an InputStream each time the sound is played.

```
InputStream soundFile =
    ResourceLoader.load( Object.class, "filepath", "respath" );
byte[] rawBytes = null;
try {
    BufferedInputStream buf = new BufferedInputStream( soundFile );
    ByteArrayOutputStream out = new ByteArrayOutputStream();
    int read;
    while ( (read = buf.read()) != -1 ) {
        out.write( read );
    }
    soundFile.close();
    rawBytes = out.toByteArray();
} catch( IOException ex ) {
    ex.printStackTrace();
}
```