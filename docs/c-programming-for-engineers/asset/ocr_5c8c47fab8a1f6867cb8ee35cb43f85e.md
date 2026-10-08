# 15.6. Reading Switch

set as an input. You must use the INPUT PULLUP option to configure the switch. In the loop, the switch state is checked using digitalRead(). If the switch is pressed (LOW state), the LED is turned on. If the switch is released (HIGH state), the LED is turned off.

The following code snippets reuses the LED blinking code from the previous section but require the built in switch to be pressed before the LED blinking can start. The first program uses a polling loop approach which acts as a barrier. It serves as a barrier, preventing further processing until the switch is pressed. Once the switch is pressed, the program proceeds to the loop() function where the LED is blinked.

```
```cpp
// Blinky2: push the button to start the LED blinking
// Uses the barrier method
```
```

```
const byte SWITCH PIN = 2;
```

```
void setup() {
    pinMode(SWITCH PIN, INPUT PULLUP);
    pinMode(LED BUILTIN, OUTPUT);
    while(digitalRead(SWITCH PIN) == HIGH);
}
```

```
void loop() {
    digitalWrite(LED BUILTIN, HIGH);
    delay(500);
    digitalWrite(LED BUILTIN, LOW);
    delay(500);
}
```

In the loop function, the LED is turned on, delayed for 500 milliseconds using delay(500), then turned off, and delayed for another 500 milliseconds.

The second program utilizes a flag variable, PROCEED, to keep track of whether the switch has been pressed. Initially, PROCEED is set to false. In the loop function, the switch input is checked, and if the switch is pressed, PROCEED is changed to true, enabling the LED blinking. Once PROCEED is set to true, it remains true and cannot be changed to false.

```
```cpp
// Blinky3: push the button to start the LED blinking
// Uses the flag variable method
```
```

```
const byte SWITCH_PIN = 2;
boolean PROCEED = false; // flag variable
```

```
void setup() {
    pinMode(SWITCH_PIN, INPUT_PULLUP);
    pinMode(LED_BUILTIN, OUTPUT);
}
```

```
void loop() {
```