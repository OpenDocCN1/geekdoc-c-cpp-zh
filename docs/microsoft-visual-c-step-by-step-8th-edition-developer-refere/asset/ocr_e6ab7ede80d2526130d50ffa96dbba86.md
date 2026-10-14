```
private async Task Say(string message)
{
    MediaElement mediaElement = new MediaElement();
    var synth = new SpeechSynthesizer();
    SpeechSynthesisStream stream =
        await synth.SynthesizeTextToStreamAsync(message);

    mediaElement.SetSource(stream, stream.ContentType);
    mediaElement.Play();
}
```