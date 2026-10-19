# 33.4 Intellectual Honesty

Part of maturing as a programming professional is developing an uncompromising sense of intellectual honesty. Intellectual honesty commonly manifests itself in several ways:

+   - Refusing to pretend you’re an expert when you’re not
+   - Readily admitting your mistakes
+   - Trying to understand a compiler warning rather than suppressing the message
+   - Clearly understanding your program—not compiling it to see if it works
+   - Providing realistic status reports
+   - Providing realistic schedule estimates and holding your ground when management asks you to adjust them

The first two items on this list—admitting that you don’t know something or that you made a mistake—echo the theme of intellectual humility discussed earlier. How can you learn anything new if you pretend that you know everything already? You’d be better off pretending that you don’t know anything. Listen to people’s explanations, learn something new from them, and assess whether they know what they are talking about.

Be ready to quantify your degree of certainty on any issue. If it’s usually 100 percent, that’s a warning sign.

> Any fool can defend his or her mistakes—and most fools do.
> —Dale Carnegie

Refusing to admit mistakes is a particularly annoying habit. If Sally refuses to admit a mistake, she apparently believes that not admitting the mistake will trick others into believing that she didn’t make it. The opposite is true. Everyone will know she made a mistake. Mistakes are accepted as part of the ebb and flow of complex intellectual activities, and as long as she hasn’t been negligent, no one will hold mistakes against her.

If she refuses to admit a mistake, the only person she’ll fool is herself. Everyone else will learn that they’re working with a prideful programmer who’s not completely honest. That’s a more damning fault than making a simple error. If you make a mistake, admit it quickly and emphatically.

Pretending to understand compiler messages when you don’t is another common blind spot. If you don’t understand a compiler warning or if you think you know what it means but are too pressed for time to check it, guess what’s really a waste of time? You’ll probably end up trying to solve the problem from the ground up while the compiler waves the solution in your face. I’ve had several people ask for help in debugging programs. I’ll ask if they have a clean compile, and they’ll say yes. Then they’ll start to explain the symptoms of the problem, and I’ll say, “Hmmmm. That sounds like it would be an uninitialized pointer, but the compiler should have warned you about that.” Then they’ll say, “Oh yeah—it did warn about that. We