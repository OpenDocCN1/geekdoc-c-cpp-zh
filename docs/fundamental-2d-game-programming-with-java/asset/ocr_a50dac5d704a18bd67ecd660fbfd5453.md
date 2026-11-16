+   - ConsoleOverlayExample combines text rendering and transparency to create a text console overlay.
+   - The SafeKeyboardInput class is added to the utility package to process typed keys without missing any. The SafeKeyboardInputExample demonstrates using the updates.

# CHAPTER 12—"THREADS"

+   - CallableTaskExample introduces using a thread pool. FileLoadingExample uses a thread pool to simulate loading resources on startup.
+   - FakeHardware, FakeHardwareListener, and FakeHardwareEvent are created to allow exploring threads with classes under your control.
+   - WaitNotifyExample demonstrates suspending and resuming threads using the wait() and notify() methods.
+   - BlockingHardware and BlockingHardwareListener demonstrate wrapping a non-blocking class with a blocking class.
+   - The BlockingQueueExample shows how to pass messages between threads.
+   - OneShotEvent, LoopEvent, and RestartEvent show how to use the BlockingHardware class in a state machine.
+   - MultiThreadEventExample explains how to use the state machines in the game loop.

# CHAPTER 13—"SOUND"

+   - PlayingClipsExample explores some of the problems with the sound support in Java.
+   - AudioStream, BlockingAudioListener, and SoundException form the base classes of the custom audio library.
+   - The BlockingClip class wraps a Clip object with a blocking class that can be used with the game code.
+   - AudioDataLine and BlockingDataLine create a blocking version of a data line for streaming sounds.
+   - SoundEvent uses a blocking queue so the sound library can be used in the game loop.
+   - OneShotEvent, LoopEvent, and RestartEvent create state machines to provide basic sound capabilities.