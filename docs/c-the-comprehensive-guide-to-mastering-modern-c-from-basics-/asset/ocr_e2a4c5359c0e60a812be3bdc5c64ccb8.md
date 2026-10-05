# # 14.1 Types of Tests

To ensure the quality of your product, you will test it. This can happen in different ways and at different stages. They are all important, and depending on the project, more or fewer tests take place at one stage or another.

You will quickly notice that with the intention of wanting to test your code in mind, you will program differently. You will want to create interfaces that simplify *automatic testing* for. Regular testing increases the quality and sustainability of your code. And if it is regular, then it should be easy to perform the test—ideally, automatically. Moreover, reproducibility is very important in tests. Because what good is it if a test fails and you cannot analyze why?

I would like to mention the following two testing types as representative of all other types of tests, as they represent the extremes:

+   - Functional and system testing
At one end of the testing spectrum, your program will be tested in its entirety. Ensure during the design and programming phases that these tests are easy to perform, reproducible, and meaningful. In practice, different flavors of these tests will occur. Here are some keywords, which by no means cover all types of tests:
  - A *smoke test* quickly checks the minimum functionality.