# Chapter 38

# Date and Time Functionality

> Time is an illusion. Lunchtime doubly so.
—Ford Prefect, the Hitchhiker' Guide to the Galaxy

This isn't too complex, but it can be a little intimidating at first, both with the different types available and the way we can convert between them.

Mix in time (UTC) and local time and we have all the Usual Fun™ one gets with times and dates.

And of course never forget the golden rule of dates and times: Never attempt to write your own date and time functionality. Only use what the library gives you.

Time is too complex for mortal programmers to handle correctly. Seriously, we all owe a point to everyone who worked on any date and time library, so put that in your budget.

# 38.1 Quick Terminology and Information

Just a quick term in case you don't have them down.

+   **UTC**: Coordinated Universal Time is a universally¹ agreed upon, absolute time. Everyone on the planet it's the same right now in UTC... even though they have different offsets.
**GMT**: Greenwich Mean Time, effectively the same as UTC². You probably want to say UTC, or "universal time". If you're talking specifically about the GMT time zone, say GMT. Confusingly, many of C's functions predict UTC and still refer to Greenwich Mean Time. When you see, that C means UTC.
**Local time**: what time is where the computer running the program is. This is described as an offset from UTC. There are many time zones in the world, most computers work in either local time or UTC.

As a general rule, if you are describing an event that happens one time, like a log entry, or a rocket launch, or pointers finally clicked for, use UTC.

On the other hand, if it's something that happens the same time in every time zone, like New Year's Eve or a lot of pain by choosing to store your dates in the wrong form.

Since a lot of languages are only good at converting UTC and local time, you can cause yourself a lot of pain by choosing to store your dates in the wrong form. (Ask me how I.)

> ¹On Earth, anyway knows what crazy systems they out there...
²OK, don't murder me! GMT is technically a time zone while UTC is a global time system. Some countries might adjust GMT for daylight saving time, whereas UTC is never adjusted for daylight saving time.