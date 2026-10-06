# Discovering Built-In Overloaded Methods

When you use the IDE to create programs, Visual Studio'sIntelliSense provides the IDE just after information about methods you are using. For example, Figure 8-21 shows how the programmer triggers the opening parenthesis to the Convert.ToInt32() method. Note the drop-down list that includes Convert.ToInt32(bool value) is 1 of 19 overloaded versions of the method. You can click the nodes to scroll through the rest of the list and see that other versions accept bool, byte, char, and so on. When retrieving an entry from a TextBox or Form, it is easy to use the Convert.ToInt32(string value) of the method, but many overloaded versions are available for ConvertBool.ToInt32() and ConvertString.ToInt32(), but having a single name with the Convert.ToInt32() that takes many different argument types makes it easier for you to remember the method name and to use it. With your work, the IDE will examine many such methods.

![](bbox=[0.102, 0.412, 0.896, 0.843])

Figure 8-21 Examining the overloaded versions of Convert.ToInt32()