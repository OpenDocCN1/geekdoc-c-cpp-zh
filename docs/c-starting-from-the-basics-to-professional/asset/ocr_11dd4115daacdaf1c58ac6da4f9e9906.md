![](bbox=[0.169, 0.179, 0.782, 0.478])

The function template starts with the template keyword to identify it as such. This is followed by a pair of angle brackets that consist of a list of one or more template parameters. In this case, there's only one, the parameter T. T is commonly used as a name for a parameter because most parameters are types, but you can use whatever name you like for a parameter; names such as type, MY_TYPE, or Comparable are equally valid. Especially if there are multiple parameters, using more descriptive names may be recommended.

The typename keyword identifies that T is a type. T is hence called a template parameter. You can also use the keyword class here—the keywords class and typename are synonymous in this context—but we prefer typename because the type argument can be a fundamental type as well, not just a class type.

The rest of the definition is similar to a normal function except that the parameter name T is sprinkled around. The compiler creates an instance of the template by replacing T throughout the definition with a specific type. The type assigned to a type parameter T during instantiation is called a template type argument.

You can position the template in a source file in the same way as a normal function definition; you can also specify a prototype for a function template. In this case, it would be as follows:

```
```cpp
template<typename T> T larger(T a, T b);  // Prototype for function template
```
```

Either the prototype or the definition of the template must appear in the source file before any statement that results in an instance of the template.

# Creating Instances of a Function Template

The compiler creates instances of the template from any statement that uses the larger() function. Here's an example:

```
```cpp
std::cout << "Larger of 1.5 and 2.5 is " << larger(1.5, 2.5) << std::endl;
```
```