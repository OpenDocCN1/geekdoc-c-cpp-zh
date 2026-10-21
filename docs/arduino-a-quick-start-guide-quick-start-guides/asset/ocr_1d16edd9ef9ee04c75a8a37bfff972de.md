We connect the button to pin 7 and the LED to pin 13 and initialize the pins accordingly in the setup() function. In loop(), we read the current state of the pin connected to the button. If it is HIGH, we turn the LED on. Otherwise, we turn it off.

Upload the program to the Arduino, and you'll see that the LED is on as long as you press the button. As soon as you release the button, the LED turns off. This is pretty cool, because now we nearly have everything we need to control our dice using our own button. But before we proceed, we'll slightly enhance our example and turn the button into a real light switch.

To build a light switch, we start with the simplest possible solution. Do not change the current circuit, and upload the following program to your Arduino:

```
```
const unsigned int BUTTON_PIN = 7;

const unsigned int LED_PIN  = 13;

void setup() {
  pinMode(LED_PIN, OUTPUT);
  pinMode(BUTTON_PIN, INPUT);
}

int led_state = LOW;

void loop() {
  const int CURRENT_BUTTON_STATE = digitalRead(BUTTON_PIN);
  
  if (CURRENT_BUTTON_STATE == HIGH) {
    led_state = (led_state == LOW) ? HIGH : LOW;
    digitalWrite(LED_PIN, led_state);
  }
}
```
```

We begin with the usual pin constants, and in setup() we set the modes of the pins we use. In line 9, we define a global variable named led_state to store the current state of our LED. It will be LOW when the LED is on and HIGH otherwise. In loop(), we check the button's current state. When we press the button, its state switches to HIGH, and we toggle the content of led_state. That is, if led_state was HIGH, we set it to LOW, and vice versa. At the end, we set the physical LED's state to our current software state accordingly.

Our solution is really simple, but unfortunately, it does not work. Play around with it a bit, and you'll quickly notice some annoying behavior.