■ Focusing on optimization during initial development detracts from achieving other program objectives. Developers immerse themselves in algorithm analysis and arcane debates that in the end don’t contribute much value to the user. Concerns such as correctness, information hiding, and readability become secondary goals, even though performance is easier to improve later than these other concerns are. Post hoc performance work typically affects less than five percent of a program’s code. Would you rather go back and do performance work on five percent of the code or readability work on 100 percent?

In short, premature optimization’s primary drawback is its lack of perspective. Its victims include final code speed, performance attributes that are more important than code speed, program quality, and ultimately the software’s users. If the development time saved by implementing the simplest program is devoted to optimizing the running program, the result will always be a program that runs faster than one developed with indiscriminate optimization efforts (Stevens 1981).

Occasionally, post hoc optimization won’t be sufficient to meet performance goals and you’ll have to make major changes in the completed code. In those cases, small, localized optimizations wouldn’t have provided the gains needed anyway. The problem in such cases isn’t inadequate code quality—it’s inadequate software architecture.

If you need to optimize before a program is complete, minimize the risks by building perspective into your process. One way is to specify size and speed goals for features and then optimize to meet the goals as you go along. Setting such goals in a specification is a way to keep one eye on the forest while you figure out how big your particular tree is.

Further Reading For many other entertaining and enlightening anecdotes, see Gerald Weinberg’s Psychology of Computer Programming (1998).

# A fast program is just as important as a correct one–false!

It’s hardly ever true that programs need to be fast or small before they need to be correct. Gerald Weinberg tells the story of a programmer who was flown to Detroit to help debug a troubled program. The programmer worked with the team who had developed the program and concluded after several days that the situation was hopeless.

On the flight home, he mulled over the situation and realized what the problem was. By the end of the flight, he had an outline for the new code. He tested the code for several days and was about to return to Detroit when he got a telegram saying that the project had been cancelled because the program was impossible to write. He headed back to Detroit anyway and convinced the executives that the project could be completed.

Then he had to convince the project’s original programmers. They listened to his presentation, and when he’d finished, the creator of the old system asked, “And how long does your program take?”

> “That varies, but about ten seconds per input.”