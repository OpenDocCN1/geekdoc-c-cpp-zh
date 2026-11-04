However, as a personal matter of taste, I still find this notation useful for UI programming, prefixing controls with their types. For one thing, the fact that controls are declared in a separate generated code file makes it more difficult to trace back the type of a control when doing code inspections outside an IDE. Furthermore, it's not uncommon to get clashes between control names and local variables. (For example, a seconds value needs to be assigned to a seconds control's Text property.)

Now that looks easy enough, doesn't it? In the Click handler, we first disable all controls to avoid multiple countdowns being active at the same time. Next we create a CountDown instance, casting the NumericUpDown's decimal-typed Value property to uint (something we know will succeed if the NumericUpDown control is configured correctly; that is, with DecimalPlaces set to 0 and its Minimum property set to 0 or more). Two event handlers are created, with help from Visual Studio upon typing +=, which causes the two methods to be generated on the fly. Notice that the explicit delegate instance creation calls can be trimmed away if you find that style clearer:

```
_countDown.Tick += _countDown_Tick;
_countDown.Finished += _countDown_Finished;
```

Code inside the handlers looks reasonable, as well, and should be self-explanatory. As you can guess, there's a little problem lurking around the corner, which is why I'm showing this example. Let's see what the problem is by simply running the program under the debugger by pressing F5. Set the number of seconds to five or so, click Start, and watch what happens. Figure 18.27 shows the result, which might not be quite as expected.

![](bbox=[0.06, 0.7, 0.75, 0.9])

FIGURE 18.27 Cross-thread access to UI controls is troublesome.

Can you guess what's going wrong based on the message? Recall how our CountDown is implemented by using a background thread. This was done to prevent the Start call from being blocked. Raising the Tick event ultimately causes method calls to all the subscribed