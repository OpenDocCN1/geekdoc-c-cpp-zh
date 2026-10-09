Another thing to note is that `Digit` is a record type. Not a struct type. In general, it is best for a value type not to include any reference type fields. It is generally hard to enforce value semantics on a value that includes any reference variables. In this particular case, however, since there is no way to update internal field, `leds`, since the constructor is private and there are no setters, we could have also used `struct`.

Note the implementation of the constructor. We simply copy the reference of the argument `leds`. If anybody else has an access to the reference variable, they can easily change the values of the elements of `leds`, which is not the behavior we desire.

In general, a better implementation would have been to "copy", or "clone", the argument array and keep the "private copy" internally. As stated, software design is about a tradeoff. Doing so would have been more expensive in terms of the computational requirements.

> The 7 LEDs are arranged in a particular order. Again, a code comment would have been nice in situations like this. Can you guess the mapping between the array indices, 0 ~ 6, and the particular LEDs?

We use the interface, `ILEDDisplay`, for "abstraction". That is, our `Clock` implementation uses the interface and we can "plug" in any `ILEDDisplay` implementations later (possibly, with some minor changes).

In this case, for instance, we may ultimately want to use our `Clock` to interface with real digital LED clocks.