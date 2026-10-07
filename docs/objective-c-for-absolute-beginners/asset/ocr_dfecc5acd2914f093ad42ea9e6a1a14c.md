5. Now, we will need to select a data type. Selecting the correct data type is very important. It will affect how your data is stored and retrieved from the database. The list has 12 items in it and can be very daunting. We will discuss the most common options, and as you become familiar with Core Data, you can experiment with the other options. The most common options are String, Integer 32, Float, and Date. For the title of the book, select String.

**String:** This is the type of attribute used to store text. This should be used to store any kind of information that is not a number or a date. In this example, the book title and author will be strings.

**Integer 32:** There are actually three different integer values for the attribute. Each of the types differ only in the minimum and maximum values possible. Integer 32 should cover most of your needs when storing an integer. An integer is a number without a decimal. If you save a decimal in an integer attribute, the decimal portion will be truncated. In this example, the year published will be an integer.

**Float:** A float is a type of attribute that can store numbers with decimals. A float is similar to a double attribute, but they differ in their minimum and maximum values. A float should be able to handle any values. In this example, we will use a float to store the price of the book.

**Date:** A date attribute is exactly what it sounds like. It allows you to store a date and time, and then performs searches and lookups based on these values. We will not use this type in this example.

6. Let's create the rest of the attributes for the book. Now, add price. It should be a float. Add the year the book was published. For two-word attributes, it is standard to make the first word lowercase and the second word initial capped. For example, an ideal name for the year the book was published would be something like, yearPublished. Select integer 32 as the attribute type. Once you have added all of your attributes, your screen should look like Figure 11–6.

NOTE: Attributes' names cannot contain spaces.