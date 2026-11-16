# LISTEN FOR HANDLED EVENTS

Well, the Window caught the MouseDown when you clicked outside a control, and the Button caught the Click event (but the Window didn't get the MouseDown), and the ListBox only behaved as expected when you clicked on the background, not on a ListBoxItem. So what happened?

Routed events aren't broken; they do work the way I've described, but there's a little wrinkle we haven't seen yet. If you look back at the class diagram for the RoutedEventArgs, you'll see a Handled property. If that's set to true inside an event handler, the event still bubbles or tunnels, but most of the handlers that are defined for the event aren't called, because the event system assumes that the handlers aren't interested unless they tell it otherwise.

Controls like the Button and RadioButton are setting the Handled property to true, so our Window-level handler isn't getting called. In fact, they're not just handling the MouseDown event; they're converting it into an entirely different event (Click). That's a pretty common pattern in WPF—controls often consume low-level input events and replace them with something a little more useful.

If you do want to know about events that some low-level object is helpfully handling for you, you can use the AddHandler() method and pass true as the HandledEventsToo parameter. Let's try it out. Take out the event handler specification in the Window XAML tag and replace it with an AddHandler() call inside the constructor.

Now run the application and test the results. Closer to what we expected, isn't it? But did you notice that the Button is no longer clicking? It reports the MouseDown, but the Click event doesn't appear to be raised at all.

![](bbox=[0.09, 0.75, 0.9, 0.89])