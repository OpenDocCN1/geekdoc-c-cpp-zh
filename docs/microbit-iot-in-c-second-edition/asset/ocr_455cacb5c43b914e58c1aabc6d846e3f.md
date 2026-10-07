You can see that in this case the degree of pull-down is greater than the pull-up, where the current is limited by the resistor. The advantage of this mode is that it can be used in an AND configuration. If multiple GPIO or other lines are connected to the output, any one of them being low will pull the output line low. Only when all of them are off the resistor succeed in pulling the line high.

# Pull-down Mode

Finally pull-down mode is exactly the same as the pull-up only now the resistor is used to pull the output line low. In the case of the pull-down mode the line is held high by the transistor but pulled low by the resistor only when all the switches are open. Putting this the other way round, the line is high if any one switch is closed.

![](bbox=[0.318, 0.373, 0.725, 0.555])

To set the mode for a GPIO line the function to use:
int setPull (PinMode pull)
where pull is any of:

+   - V1 Pullup Pulldown PullNone
- V2 PullMode::Up PullMode::Down PullMode::None

PullNone is the default and the value of the pull-up/down resistor is in the range 10 to 16K. What this means is that in most cases you will probably have to add an external pull-up/down resistor to bring the resistance down.