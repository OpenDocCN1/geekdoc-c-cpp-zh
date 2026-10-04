Figure 7-4:
Class factoring can (and usually does) result in added layers of inheritance hierarchy.

![](bbox=[0.22, 0.14, 0.83, 0.44])

You can see that I have inserted a pair of new classes between University and School: HigherLearning and LowerLevel. For example, I've subdivided the new class HigherLearning into College and University. This type of multitiered class hierarchy is common and desirable when factoring out relationships. They correspond to reality, and they can teach you sometimes subtle features of your solution.

Note, however, that no Unified Factoring Theory exists for any given set of classes. The relationship shown in Figure 7-4 seems natural, but suppose that an application cared more about differentiating types of schools that are administered by local politicians from those that aren't. This relationship, shown in Figure 7-5, is a more natural fit for that type of problem. No “correct” factoring exists: The proper way to break down the classes is partially a function of the problem being solved.

Figure 7-5:
Breaking down classes is partially a function of the problem being solved.

![](bbox=[0.22, 0.66, 0.83, 0.9])