![](bbox=[0.17, 0.09, 0.74, 0.37])

# Figure 3.12: We have a winner!

Bounce class for the first time. To determine the current state of our guess_button object, we have to call its update() method. afterward, we read its current status using the read() method.

If the button was pressed, its state is set to HIGH, and we increment the guess variable. To make sure that the guess is always in the range between 1 and 6, we use the modulus operator (%) in line 33. This operator divides two values and returns the remainder. For 6, it returns values between 0 and 5, because when you divide a number by 6, the remainder is always between 0 and 5. Add 1 to the result, and you get values between 1 and 6. Finally, we output the current guess using the three LEDs, and we also print it to the serial port.

The handling of the start button in handle_start_button() works exactly the same as the handling of the guess button. When the start button was pressed, we calculate a new result and output it on the serial port. Then we check whether the user has entered a guess (guess is greater than zero in this case) and whether the user has guessed the right result. In either case, we print a message to the serial port, and if the user guessed right, we also call the hooray() method. hooray() lets all three LEDs blink several times.