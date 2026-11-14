# # Chapter 4 Libraries

> > "God, grant me the serenity to accept the things I cannot change,
> > The courage to change the things I can,
> > And the wisdom to know the difference"
> > —Reinhold Niebuhr

We as programmers need similar strengths. We have great visions of what our software should accomplish, and we need very strong Courage to make this happen. Nonetheless, a day has only 24 hours and even hardcore geeks eat and sleep sometimes. As a consequence, we cannot program everything we dream of (or are paid for) by ourselves and have to rely on existing software. Then we have to Accept what this software provides us by implementing interfaces with appropriate pre- and post-processing. The decision whether to use existing software or write a new program requires all our Wisdom.

Actually, it even requires some prophetic powers to rely on software without having years of experience with it. Sometimes, packages work well at the beginning, and once we build a larger project on top of it, we may experience some serious problems that cannot be compensated for easily. Then we might realize painfully that another software package or an implementation from scratch would have been the better option.

The C++ standard library might not be perfect, but it is designed and implemented very carefully so that we can prevent such bad surprises. The components of the standard library pass the same thorough evaluation process as the features of the core language and guarantee the highest quality. The library standardization also assures that its classes and functions are available on every compliant compiler. We already introduced some library components before, like initializer lists in §2.3.3 or I/O streams in §1.7. In this chapter, we will present more library components that can be very useful for the programming scientist or engineer.

A comprehensive tutorial and reference for the standard library in C++11 is given by Nicolai Josuttis [26]. The fourth edition of Bjarne Stroustrup’s book [43] covers all library components as well, although in a little less detail.

Furthermore, there are many scientific libraries for standard domains like linear algebra or graph algorithms. We will briefly introduce some of them in the last section.

# ## 4.1 Standard Template Library

The Standard Template Library (STL) is the fundamental generic library for containers and algorithms. Every programmer should know it and use it when appropriate instead of reinventing the wheel. The name might be a bit confusing: most parts of the STL as