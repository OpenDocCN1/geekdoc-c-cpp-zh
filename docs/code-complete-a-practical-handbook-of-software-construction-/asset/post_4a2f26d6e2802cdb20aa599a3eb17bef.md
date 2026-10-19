
One definition of engineering is to do for a dime what anyone can do for a dollar. Iterating in the late stages is doing for two dollars what anyone can do for one dollar. Fred Brooks suggested that you “build one to throw away; you will, anyhow” (Brooks 1995). The trick of software engineering is to build the disposable parts as quickly and inexpensively as possible, which is the point of iterating in the early stages.

## 34.9 Thou Shalt Rend Software and Religion Asunder

Religion appears in software development in numerous incarnations—as dogmatic adherence to a single design method, as unswerving belief in a specific formatting or commenting style, or as a zealous avoidance of global data. Whatever the case, it’s always inappropriate.

### Software Oracles

Cross-Reference: For details on handling programming religion as a manager, see “Religious Issues” in Section 28.5.

Unfortunately, the zealous attitude is decreed from on high by some of the more prominent people in the profession. It’s important to publicize innovations so that practitioners can try out promising new methods. Methods have to be tried before they can be fully proven or disproved. The dissemination of research results to practitioners is called “technology transfer” and is important for advancing the state of the practice of software development. There’s a difference, however, between disseminating a new methodology and selling software snake oil. The idea of technology transfer is poorly served by dogmatic methodology peddlers who try to convince you that their new one-size-fits-all, high-tech cow pies will solve all your problems. Forget everything you’ve already learned because this new method is so great it will improve your productivity 100 percent in everything!

Rather than latching on to the latest miracle fad, use a mixture of methods. Experiment with the exciting, recent methods, but bank on the old and dependable ones.

### Eclecticism

Cross-Reference: For more on the difference between algorithmic and heuristic approaches, see Section 2.2, “How to Use Software Metaphors.” For information on eclecticism in design, see “Iterate” in Section 5.4.

Blind faith in one method precludes the selectivity you need if you’re to find the most effective solutions to programming problems. If software development were a deterministic, algorithmic process, you could follow a rigid methodology to your solution. But software development isn’t a deterministic process; it’s heuristic, which means that rigid processes are inappropriate and have little hope of success. In design, for example, sometimes top-down decomposition works well. Sometimes an object-oriented approach, a bottom-up composition, or a data-structure approach works better. You have to be willing to try several approaches, knowing that some will fail and some will succeed but not knowing which ones will work until after you try them. You have to be eclectic.

Adherence to a single method is also harmful in that it makes you force-fit the problem to the solution. If you decide on the solution method before you fully understand the problem, you act prematurely. Over-constrain the set of possible solutions, and you might rule out the most effective solution.

You’ll be uncomfortable with any new methodology initially, and the advice that you avoid religion in programming isn’t meant to suggest that you should stop using a new method as soon as you have a little trouble solving a problem with it. Give the new method a fair shake, but give the old methods their fair shakes, too.

Cross-Reference: For a more detailed description of the toolbox metaphor, see “Applying Software Techniques: The Intellectual Toolbox” in Section 2.3.

Eclecticism is a useful attitude to bring to the techniques presented in this book as much as to techniques described in other sources. Discussions of several topics presented here have advanced alternative approaches that you can’t use at the same time. You have to choose one or the other for each specific problem. You have to treat the techniques as tools in a toolbox and use your own judgment to select the best tool for the job. Most of the time, the tool choice doesn’t matter very much. You can use a box wrench, vise-grip pliers, or a crescent wrench. In some cases, however, the tool selection matters a lot, so you should always make your selection carefully. Engineering is in part a discipline of making tradeoffs among competing techniques. You can’t make a tradeoff if you’ve prematurely limited your choices to a single tool.

The toolbox metaphor is useful because it makes the abstract idea of eclecticism concrete. Suppose you were a general contractor and your buddy Simple Simon always used vise-grip pliers. Suppose he refused to use a box wrench or a crescent wrench. You’d probably think he was odd because he wouldn’t use all the tools at his disposal. The same is true in software development. At a high level, you have alternative design methods. At a more detailed level, you can choose one of several data types to represent any given design. At an even more detailed level, you can choose several different schemes for formatting and commenting code, naming variables, defining class interfaces, and passing routine parameters.

A dogmatic stance conflicts with the eclectic toolbox approach to software construction. It’s incompatible with the attitude needed to build high-quality software.

### Experimentation

Eclecticism has a close relative in experimentation. You need to experiment throughout the development process, but zealous inflexibility hobbles the impulse. To experiment effectively, you must be willing to change your beliefs based on the results of the experiment. If you’re not willing, experimentation is a gratuitous waste of time.

Many of the inflexible approaches to software development are based on a fear of making mistakes. A blanket attempt to avoid mistakes is the biggest mistake of all. Design is a process of carefully planning small mistakes in order to avoid making big ones. Experimentation in software development is a process of setting up tests so that you learn whether an approach fails or succeeds—the experiment itself is a success as long as it resolves the issue.

Experimentation is appropriate at as many levels as eclecticism is. At each level at which you are ready to make an eclectic choice, you can probably come up with a corresponding experiment to determine which approach works best. At the architectural-design level, an experiment might consist of sketching software architectures using three different design approaches. At the detailed-design level, an experiment might consist of following the implications of a higher-level architecture using three different low-level design approaches. At the programming-language level, an experiment might consist of writing a short experimental program to exercise the operation of a part of the language you’re not completely familiar with. The experiment might consist of tuning a piece of code and benchmarking it to verify that it’s really smaller or faster. At the overall software-development-process level, an experiment might consist of collecting quality and productivity data so that you can see whether inspections really find more errors than walk-throughs.

The point is that you have to keep an open mind about all aspects of software development. You have to get technical about your process as well as your product. Open-minded experimentation and religious adherence to a predefined approach don’t mix.

### Key Points

- One primary goal of programming is managing complexity.
- The programming process significantly affects the final product.
- Team programming is more an exercise in communicating with people than in communicating with a computer. Individual programming is more an exercise in communicating with yourself than with a computer.
- When abused, a programming convention can be a cure that’s worse than the disease. Used thoughtfully, a convention adds valuable structure to the development environment and helps with managing complexity and communication.
- Programming in terms of the problem rather than the solution helps to manage complexity.
- Paying attention to intellectual warning signs like the “irritation of doubt” is especially important in programming because programming is almost purely a mental activity.
- The more you iterate in each development activity, the better the product of that activity will be.
- Dogmatic methodologies and high-quality software development don’t mix. Fill your intellectual toolbox with programming alternatives, and improve your skill at choosing the right tool for the job.
