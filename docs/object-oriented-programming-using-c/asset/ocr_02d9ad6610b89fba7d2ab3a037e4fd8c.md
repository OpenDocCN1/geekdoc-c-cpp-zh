Object Oriented Programming using C#

Agile Programming

# 10.9 Examples of Assertions

When setting up test cases we make assertions. An assertion is a statement which should be true if the code has functioned correctly. Example of assertion include ...

+   - Assert.AreEqual(...)
- Assert.AreNotEqual(...)
- Assert.Fail(...)
- Assert.IsTrue(...)
- Assert.IsFalse(...)

Assert.AreEqual() and Assert.Fail() will be adequate for many testing purposes, as we will see here.

Assert.Fail() indicates that having reached this line means the test failed! While we say the test has failed this is not strictly true. It is not the test that failed but our code that failed. The test successfully found an error in our code.

![](bbox=[0.125, 0.513, 0.941, 0.893])

Here at Ericsson we have a deep rooted belief that the innovations we make on a daily basis can have a profound effect on making the world a better place for people, business and society. Join us.

In Germany we are especially looking for graduates as Integration Engineers for
- Radio Access and IP Networks
- IMS and IPT

We are looking forward to getting your application! To apply and for all current job openings visit our web page: www.ericsson.com/careers