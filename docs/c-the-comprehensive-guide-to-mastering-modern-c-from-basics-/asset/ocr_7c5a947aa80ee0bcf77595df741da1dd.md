I won't hide it: templates are difficult. But I want to make it easy for you, because if you completely avoid templates, you will miss out on most of the good things in C++.

The good news: You don't need to fully understand templates to use them. I would even argue that there are few people who have completely understood templates. However, you can still use them without too much mental gymnastics and thus get the most benefit from them. In fact, you have already used templates—namely, string. And I very much hope that you have come to know and love string by now. The second faithful companion through many pages of this book, with whose help you have already used templates, vector—in its vector<int>, vector<double>, or even vector<Car> form.

So you have already dealt with the first aspect of templates: you use them as parameterized types. And that's exactly what a template is: a class that takes another type as a parameter is a class template. vector is one of them, and so is basic_string. Give basic_string a char as a parameter, and you get this:

```
using string = basic_string<char>;
```

Voilà! This is simplified, because basic_string can do a bit more. I will explain how to create templates—the class templates—once you have learned about function templates.