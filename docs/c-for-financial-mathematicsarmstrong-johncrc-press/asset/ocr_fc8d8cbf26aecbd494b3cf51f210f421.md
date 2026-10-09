tell you about it quickly. This is important because it is much easier to fix a bug shortly after you have written it. You may even find that you can hardly remember precisely what code changes you have made after a couple of hours have passed. This will obviously make debugging much harder. To help with this, write lots of unit tests and make sure all your tests are run whenever you change your code (see Section 15.4.5).

As important as telling you which parts of your code are currently not working, unit tests tell you which parts of your code *are working*. If you have a million lines of code, knowing which parts of code you need to think about is extremely important.

Whenever you discover a bug in your code that *wasn’t* picked up by a unit test you should write a unit test to make sure it never happens again. You should never write new code unless you are also writing tests for it.

**Tip: Write a little, test a little.**

Do not write large amounts of code in one sitting. Write a small amount of code. Write some tests. Make sure everything compiles and all the tests pass. Then back up your code using your version control system (see Section 15.4.1). That way when an error occurs you should have a clear idea of what you are doing that might have caused it.

# 15.1.2 Reading your code

Often the quickest way to find a bug in your code is to read it through. This approach will only work if you know already which function contains the error as you cannot possibly re-read all your code every time a bug occurs. However, if you are following the strategy of writing a little and testing a little, you can usually guess that the bug is in the code you have just written.

Very often it helps to explain your code to someone else. A very effective development practice is to write your code with a colleague. This is called pair programming [1]. You will find that you and your colleague both learn from each other and that many bugs are spotted before the code is even executed.

Some people suggest an alternative practice called code-review, where developers read each other’s code and comment on it. This is much less enjoyable than pair programming and, it is argued in [1], much less effective.

# 15.1.3 Logging statements

You have probably already discovered for yourself the strategy of inserting logging statements throughout your code. By printing out the values of different variables at each line, one can often quickly work out what is going wrong.

You may find that you are regularly inserting and deleting logging state-