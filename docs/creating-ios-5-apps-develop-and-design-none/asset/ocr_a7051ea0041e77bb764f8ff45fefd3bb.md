Both setTitle:forState: and setTitleColor:forState: refer to the button's state. Every control has a state: normal, highlighted, selected, or disabled. Different actions can change the control's state (see Table 4.2). Our button uses only two. It is highlighted when touched; otherwise, it is normal.

When setting per-state attributes, if you don't explicitly assign a value to a given state, that state will default back to the UIControlStateNormal setting. For example, in our code we only had to set the title once. Unless we say otherwise, every other state will use this value as well.

This brings up a point that is often confused. If you look up UIControlState in the developer documentation, the enum is designed as a bitmask. This means we should be able to combine multiple states using the bitwise OR operator (|). As a result, you might be tempted to explicitly set the title for all the states using code like this:

```
```
UIControlState all = UIControlStateNormal |
                     UIControlStateSelected |
                     UIControlStateHighlighted |
                     UIControlStateDisabled;
[self.button setText:@"default text" forState:all]
```
```

Unfortunately, this does not work. Instead of setting the title for all states, you are actually setting the title for a single state: specifically, the state in which the control is selected, highlighted, and disabled—all at the same time (in this case, UIControlStateNormal is ignored).

This can be handy when creating things like custom two-state buttons. These buttons have an ON and an OFF state, and each of these states can be displayed either normally or highlighted. This means we need to define four different appearances for these four different states.

We can use the button's selected property to indicate its ON/OFF state. Our appearances are then defined as follows: UIControlStateNormal means the button is OFF; UIControlStateHighlighted means the button is OFF and touched; UIControlStateSelected means the button is ON; and UIControlStateHighlighted | UIControlStateSelected means the button is both ON and touched (Figure 4.11). Note that UIControlStateDisabled is not used here.