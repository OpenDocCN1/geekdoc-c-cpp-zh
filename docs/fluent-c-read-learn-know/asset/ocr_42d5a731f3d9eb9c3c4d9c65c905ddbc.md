# # USING STRATEGY

We've learned from our chefs that different categories of baked goods change their yield using different methods. If we use inheritance for all the different possibilities, we're going to have a problem:

![](bbox=[0.09, 0.205, 0.75, 0.765])

Using classical inheritance, we'd create a lot of classes that differ only slightly. It's easy to see how the class hierarchy could get really cluttered really quickly. (There are different categories of cakes and bread, for example, each of which would need a different class.)

The other problem here is that if the semantics of the ChangeYield() function changes (say, for example, you decide that you need another parameter), you have to fix it in lots of different places. That's potentially a lot of repetitive work. Who needs that?