In Ruby, certain methods that return true or false may be referenced as a question. For instance "frozen?" will return true if the object is frozen, or false if it is not. This is a style convention and some folks will use it if and others will use if statement. The inline question mark can be used for more complicated if statements as well. One such example is an inline if statement. This allows you to return a variable from an if statement using a single line.

```
>> myList = [{ :name => "Ruby" }, {:name => "RuleZ"}]
=> [{:name=>"Ruby"}]
>> myList.each { |i| print i.keys.first.object_id.to_s\"" }
66088
66088
=> [{name=>"Ruby"},{name=>"RuleZ"}]
```

Here, we substitute symbols to define the key name. Symbols start with the symbol and dont require any quotations. This time, we iterate through keys we see that both times used: name the key had the same object ID. This shows, by using symbols, that we are using the same object instance, and therefore using less memory. Visually, the symbol class also allows the keys and values to be easily identified and is a good convention to maintain for programming.

# Constants, integers, and floats

We have now seen arrays, hashes, symbols, and strings. Let's take a look at constants, integers, and floats.

Like Python, Ruby treats integers and floating-point numbers differently. As a result, many of the same integer division tricks we used with Python in Chapter 2, Introduction to Python, will still work. In our next code example, we start by setting values for our variables a and b to integer values. When we try divide these values we end up with a rounded answer in integer form. In order to get the answer in the form of a floating-point number, we have to use the to_f method of the integer class to convert each number to a floating-point number. We can assign that number to our MyConstant variable.