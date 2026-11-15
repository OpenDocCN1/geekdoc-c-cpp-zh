# # 10 Exception Handling

CHAPTER 4 DISCUSSED using the try/catch/finally blocks for standard exception handling. In that chapter, the catch block always caught exceptions of type System.Exception. This chapter defines some additional details of exception handling—specifically, details surrounding additional exception types, defining custom exceptions, and multiple catch blocks for handling each type. This chapter also details exceptions because of their reliance on inheritance.

![](bbox=[0.25, 0.57, 0.8, 0.77])

# ## Multiple Exception Types

Listing 10.1 throws a System.ArgumentException, not the System.Exception type demonstrated in Chapter 4. C# allows code to throw any type that derives (perhaps indirectly) from System.Exception.