# Table 1.10 Example of an Ill-Structured Problem

| Travel Agent's Questions | Responses |
|---|---|
| Can I help you? | I'm not sure. |
| Where do you want to go? | Somewhere. |
| Any particular destination? | Here and there. |
| How much can you afford? | I don't know. |
| Can you get some money? | I don't know. |
| When do you want to go? | Sooner or later. |

In dealing with ill-structured problems, there is a danger that the expert system design may accidentally develop into an algorithmic solution. If there is a good algorithm, there is no need for an expert system. A clue that this has happened occurs if a solution is found that requires a rigid control structure. That is, the rules are forced to execute in a certain sequence by the knowledge engineer explicitly setting the priorities of many rules. Forcing a rigid control structure on the expert system cancels a major advantage of expert systems technology, which is dealing with unexpected input that does not follow a predetermined pattern. That is, expert systems react opportunistically to their input, whatever it is. Conventional programs generally expect input to follow a certain sequence. An expert system with a lot of control often indicates a disguised algorithm and may be a good candidate for recoding as a conventional program.

+   * Is the domain well bounded? It is very important to have well-defined limits on what the expert system is expected to know and what its capabilities should be. For example, suppose you wanted to create an expert system to diagnose headaches. Certainly medical knowledge of a physician would be put in the knowledge base. However, for a deep understanding of headaches, you might also put in knowledge about neurochemistry, then its parent area of biochemistry, then chemistry, molecular biophysics, and so forth, perhaps down to subnuclear physics. Other domains such as biofeedback, psychology, psychiatry, physiology, exercise, yoga, and stress management may also have pertinent knowledge about headaches. The point of all this is—when do you stop adding domains? The more domains, the more complex the expert system becomes.

In particular, the task of coordinating all the expertise becomes a major task. In the real world, we know from experience how difficult it is to have coordinated teams of experts working on problems, especially when they come up with conflicting recommendations. If we knew how to program well the coordination of expertise, then we could try programming an expert system to have the knowledge of multiple experts. The first attempts made to coordinate multiple expert systems were the HEARSAY II and HEARSAY III systems. These projects demonstrated the complexity of the task. As a familiar example, try bringing your car into multiple service centers when you have a problem and note how many disparate diagnoses you get. As expertise becomes more scarce, so