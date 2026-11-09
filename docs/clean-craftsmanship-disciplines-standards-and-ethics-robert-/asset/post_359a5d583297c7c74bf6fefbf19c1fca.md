
But wait. Did you know that there is a better algorithm for calculating sines? It’s called CORDIC. No, I’m not going to describe it to you here. It’s way beyond the scope of this chapter. But let’s just say that we wanted to change our function to use that CORDIC algorithm.

Our spy tests would break!

In fact, just look back at how much code we invested in that Taylor series algorithm. We’ve got two whole classes, the `SineTaylorCalculator` and the `SineTaylorCalculatorSpy`, dedicated to our old algorithm. All that code would have to go away, and a whole new testing strategy would have to be employed.

The spy tests are *fragile*. Any change to the algorithm breaks virtually all those tests, forcing us to fix or even rewrite them.

On the other hand, if we’d stayed with our original value tests, then they would continue to pass with the new CORDIC algorithm. No rewriting of tests would be necessary.

Welcome to the second half of the TDD uncertainty principle. If you demand certainty from your tests, you will inevitably couple your tests to the implementation, and that will make the tests fragile.

> *The TDD uncertainty principle: To the extent you demand certainty, your tests will be inflexible. To the extent you demand flexible tests, you will have diminished certainty.*

### London versus Chicago

The TDD uncertainty principle might make it seem that testing is a lost cause, but that’s not the case at all. The principle just puts some constraints on how beneficial our tests can be.

On the one hand, we don’t want rigid, fragile tests. On the other hand, we want as much certainty as we can afford. As engineers, we have to strike the right trade-off between these two issues.

### The Fragile Test Problem

Newcomers to TDD often experience the problem of fragile tests because they are not careful to design their tests well. They treat the tests as second-class citizens and break all the coupling and cohesion rules. This leads to the situation where small changes to the production code, even just a minor refactoring, cause many tests to fail and force sweeping changes in the test code.

Failed tests that necessitate significant rewriting of test code can result in initial disappointment and premature rejection of the discipline. Many young, new TDDers have walked away from the discipline simply because they failed to realize that tests have to be designed just as well as the production code.

The more you couple the tests to the production code, the more fragile your tests become; and few testing artifacts couple more tightly than spies. Spies look deep into the heart of algorithms and inextricably couple the tests to those algorithms. And since mocks are spies, this applies to mocks as well.

This is one of the reasons that I don’t like mocking tools. Mocking tools often lead you to write mocks and spies, and that leads to fragile tests.

### The Certainty Problem

If you avoid writing spies, as I do, then you are left with value and property testing. Value tests are like the sine value tests we did earlier in this chapter. They are just the pairing of input values to output values.

Property tests are like the `testSineInRange` and `PythagoreanIdentity` tests we used earlier. They run through many appropriate input values checking for invariants. These tests can be convincing, but you are still often left with a nagging doubt.

On the other hand, these tests are so decoupled from the algorithm being employed that changing that algorithm, or even just refactoring that algorithm, cannot affect the tests.

If you are the kind of person who values certainty over flexibility, you’ll likely use a lot of *spies* in your tests and you’ll tolerate the inevitable fragility.

humble opinion.

## Synthesis

Although these two schools of thought exist, and although there are practitioners who tend toward one side or the other, London versus Chicago is not a war. It’s not really even much of a disagreement. It is a minor point of emphasis, and little more.

Indeed, all practitioners, whether Chicagoans or Londoners, use both techniques in their work. It’s just that some do a little more of one, and some do a little more of the other.

Which is right? Neither, of course. I tend more toward the Chicago side, but you may look at the London school and decide you are more comfortable there. I have no disagreement with you. Indeed, I will happily pair program with you to create a lovely synthesis.

That synthesis becomes very important when we start to consider architecture.

## Architecture

The trade-off I make between the London and Chicago strategies is architectural. If you read *Clean Architecture*,^4 you know that I like to partition systems into components. I call the divisions between those components *boundaries*. My rule for boundaries is that source code dependencies must always cross a boundary pointing toward high-level policy.

4. Robert C. Martin, *Clean Architecture: A Craftsman’s Guide to Software Structure and Design* (Addison-Wesley, 2018).

This means that components that contain low-level details, like graphical user interfaces (GUIs) and databases, depend on higher-level components like business rules. High-level components do not depend on lower-level components. This is an example of the dependency inversion principle, which is the D in SOLID.

When writing the lowest-level programmer tests, I will use *spies* (and rarely *mocks*) when testing across an architectural boundary. Or, to say that a different way, when testing a component, I use *spies* to mock out any collaborating components and to ensure that the component I am testing invokes the collaborators correctly. So, if my test crosses an architectural boundary, I’m a Londoner.

However, when a test does not cross such a boundary, I tend to be a Chicagoan. Within a component, I depend much more on state and property testing in order to keep the coupling, and therefore the fragility, of my tests as low as possible.

Let’s look at an example. The UML diagram in **Figure 3.8** shows a set of classes and the four components that contain them.

![](img/7b01f9dd5d5d33f16ee27a44427cd56e_170_0.png)

**Figure 3.8** A set of classes and the four components that contain them

Note that the arrows all point from lower-level components to higher-level components. This is the *Dependency Rule* that is discussed in *Clean Architecture*. The highest-level component contains the business objects. The next level down contains the interactors and the communications interfaces. At the lowest level is the GUI and the database.

We might use some stubs when testing the business objects, but we won’t need any spies or mocks because the business objects don’t know about any other components.

The interactors, on the other hand, manipulate the business objects, the database, and the GUI. Our tests will likely use spies to make sure that the database and GUI are being manipulated properly. However, we will probably not use as many spies, or even stubs, between the interactors and the business objects because the functions of the business objects are probably not expensive.

When testing the controller, we will almost certainly use a spy to represent the interactor because we don’t want the calls to propagate to the database or presenter.

The presenter is interesting. We think of it as part of the GUI component, but in fact we’re going to need a spy to test it. We don’t want to test it with the real view, so we probably need a fifth component to hold the view apart from the controller and presenter.

That last little complication is common. We often modify our component boundaries because the tests demand it.

## Conclusion

In this chapter, we looked at some of the more advanced aspects of TDD: from the incremental development of algorithms, to the problem of getting stuck, from the finite state machine nature of tests to test doubles and the TDD uncertainty principle. But we’re not done. There’s more. So, get a nice hot cup of tea and turn the improbability generator up to infinity.
