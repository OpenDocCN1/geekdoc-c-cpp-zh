a new C++ standard obviously had to take care not to compromise older code through incompatible changes. There are billions of lines of C++ code in use that the committee must not break. Stability over decades is an essential “feature.”

C++11 added massively to the standard library and pushed to complete the feature set needed for a programming language that is a synthesis of the “paradigms” and idioms that had proven successful with C++98.

The overall aims for the C++11 effort were:

+   - Make C++ a better language for systems programming and library building.
- Make C++ easier to teach and learn.

The aims are documented and detailed in [Stroustrup, 2007].

A major effort was made to make this model {18.1} and support for lock-free programming. This was the work of Hans Boehm, Brian McKnight, and others in the concurrency working group. On top of that, we added the threads.

After C++11 there was wide agreement that 13 years between standards were far too many. Herb Sutter proposed that the committee adopt a policy of shipping on time at fixed intervals, the “train model.” I argued for a short interval to minimize the change of delays because someone insisted on extra time to allow inclusion of “just one more essential feature.” We agreed on an ambitious 3-year schedule that we would alternate between minor and major releases.

C++14 was deliberately a minor release “completing C++11”. This reflects the reality that with a release date, there will be features that we know, but can’t deliver on time. Once, in widespread use, gaps in the feature set will inevitably be discovered.

C++17 was meant to be a major release. By “major,” I mean containing features that change the way we think about the structure of our software and how we design it. By definition, C++17 was at a minimum release. alot of minor extensions, the features that would have had dramatic changes (e.g., concepts, modules, and coroutines) were either not ready or made in controversy and lack of design direction. As a result, C++ programmer who had already absorbed the lessons of C++11 and C++14.

C++20 offers long-promised and much-needed major features, such as modules {3.2.2}, concepts ({8.2}), ranges ({18.6}, {14.5}), and many minor features. It is as a major upgrade to C++ as C++11. It became widely available in late 2021.

The ISO standards committee, SC22/WG21, has about 350 members, out of which about 250 attended the last pre-pandemic face-to-face meeting in Prague C++20 was approved by a unanimous 79-0 that was ratified by a national body vote of 22-0. Getting that degree of agreement among a large and diverse group is hard. Dangers include “Design by committee,” feature bloat, lack of consistent style, and short-sighted decisions. Making progress toward simpler and more coherent language is very hard. The committee is aware of and trying to counter it; [Wong, 2020]. Sometimes, we succeed and it is very hard to avoid complexity creeping in from “minor features,” fashion, and the desire of experts to serve rare special cases directly.