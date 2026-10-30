# Prioritize consistency

Arguing on the Internet is a complete and utter waste of time and energy. It is futile and illogical. Yet, despite being a category of people who rely on their keen sense of logic, software developers often argue on the Internet. From the pedantry of the perfect sort of algorithm to “best language” flame wars, developers cannot help but launch themselves headlong into pointless arguments.

The truth is, on a practical level, you have infinite choices available to you. You cannot hope to critically evaluate all of them at all times; therefore, a better heuristic is needed. The first principle that should be upheld in any codebase is *consistency*. This applies to a multitude of areas.

Do not argue with each other over the relative benefits of preceding underscores for class field names versus ubiquitous use of this. Instead, be consistent, and follow the example already set by the code. Any time lost arguing is better spent making real, actual, tangible progress.

This applies throughout the codebase. Test code, however, generates the most heated of debates.

This is all very well in a brownfield project that is already internally consistent, but what about greenfield projects or projects that are ambiguous about their patterns? For greenfield projects, make a decision that is most agreeable and stick to it. When a project’s code already exhibits a mixture of naming conventions or applicable patterns, choose the most common example and slowly normalize the rest of the code to match.

# Maintain a reasonable test fixture per class ratio

A 1:1 ratio of test fixture to production class should suffice in most cases. Using a single test fixture to exercise more than one system under test is confusing and breaks the Principle of Least Astonishment. This is much the same as putting multiple classes in a single file: it is something that should be avoided lest others have difficulty navigating the code.

> **Tip**  The *Principle of Least Astonishment* is a guideline recommending that you choose the simplest, most obvious choice when presented with a decision. It aims to make life easier for those who come after you—perhaps even a future version of yourself who might be astonished at an odd decision!

# Name the system under test

Although abbreviations should generally be avoided when writing code, naming the variable that represents the system under test at least benefits from being consistent. Even if an alternative name is chosen, such as target, a consistent name across all tests allows the next readers of your code to orient themselves quickly.