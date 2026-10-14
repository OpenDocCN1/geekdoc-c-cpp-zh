```
SpeechRecognitionResult speechRecognitionResult = ...;
string commandMode = speechRecognitionResult.SemanticInterpretation.Properties["commandMode"].FirstOrDefault();
```