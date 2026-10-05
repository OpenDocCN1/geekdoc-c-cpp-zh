+   - Function name
This is a regular identifier under which you will later use the function. It may be that your function belongs to a class (method), in which case the function name is made up of ClassName::Method. Also, when you get to know function templates later, the name may be followed by angle brackets <...>. I will cover this in Chapter 23.

+   - Parameters
If your function does not take any parameters, the parentheses are empty (). Otherwise, the types and names of the function parameters are listed here, separated by commas.

+   - Parameter type
Each parameter must be specified with at least its type. The abundance of possible types ranges from simple ones (such as int and std::string) to complex ones with several angle brackets (such as map<string,vector<int>>). It is particularly important to distinguish whether you want to specify a parameter as a reference or pointer; in the latter two cases, & or * is part of the type. If the parameter cannot be modified within the function, const is part of the type.

+   - Parameter name
To be able to use the parameter in the function at all, refer to it by the name given here. You can omit it if you are only declaring the function here (and not defining it) or if you do not use the parameter in the function at all. However, I recommend using a clear,