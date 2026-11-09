Look back at that UML diagram. We could have divided out the tasks to three or four programmers and integrated a day or two later. And the tragedy is that we’d have gotten it working. We would have celebrated the 400<sup>6</sup> lines of working code, never knowing that the algorithm was a `for` loop and two `if` statements that fits into 14 lines of code.

6. I know it’s 400 lines of code because I’ve written it.

Did you see the solution early? Did you see the `for` loop and two `if` statements? Or did you expect one of the tests to eventually force me to write the `Frame` class? Were you holding out for the tenth frame? Is that where you thought all the complexity would be found?

Did you know we were done before we ran the tenth frame test? Or did you think there was a lot more to do? Isn’t it fascinating that we can write a test fully expecting more work ahead, only to find, to our surprise, that we are done?

Some folks have complained that if we’d followed the UML diagram shown earlier, we’d have wound up with code that was easier to change and maintain. That’s pure bollocks! What would you rather maintain, 400 lines of code in four classes or 14 lines with a `for` loop and two `if` statements?

# Conclusion

In this chapter, we studied the motivations and basics of TDD. If you’ve gotten this far, your head may be spinning. We covered a lot of ground. But not nearly enough. The next chapter goes significantly deeper into the topic of TDD, so you may wish to take a little rest before turning the page.