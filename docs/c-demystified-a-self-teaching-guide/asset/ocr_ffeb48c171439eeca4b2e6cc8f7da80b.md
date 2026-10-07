# Data Types

The ones and zeroes that may be stored at a memory address may represent text, such as my name, Jeff Kent. These ones and zeroes instead may represent a number, as my height in inches, 72, or a number with digits to the decimal point, as my GPA in high school, I'll say I was 37.5 (honestly don't remember, it was too long ago). Alternatively, the ones and zeroes may represent either true or false, as I I a U.S. citizen.

Data comes in many forms, and is generally either numeric or textual. Additionally, some numeric data uses these numbers, such as 6, 0, or –7, while other numeric data uses floating-point numbers, such as 6., and -6.1.

There are different data types for each of the many forms of data. The data type you choose will affect not only the form in which the data is stored, but also the amount of memory required to store it. Let's now take a look at these different data types.

# Whole Number Data Types

We deal with numbers all the time. Think of the answers to questions such as how many cars are in the parking lot, how many classes are you taking, or how many brothers and sisters do you have? Each answer involves a number, with no need to express any value to the decimal point. After all, who has 31 brothers and sisters?

Often, you don't need a large number. What unfortunate student would need 754,361 classes at most one. However, the whole number needs to be large. For example, if you are studying astronomy, the moon is approximately 240,000 miles from Earth. Indeed, the whole number may need to be very, very. Pluto's minimum distance from Earth is about 2.7 billion miles.

Many times, the whole number won't be negative. No matter how badly you do on a test, chances are you won't score below zero points. However, some numbers may be below zero, such as the temperature at the North Pole.

Because of the different needs numbers may have many, there are several different number data types (shown in Table 2-2). The listed sizes and ranges are typical, but may vary depending on the compiler and operating system. In the size/operator section later in this chapter, you will determine through code the different data types on your compiler and operating system.

# Table 2-2: Whole Number Data Types, sizes, and Ranges

| Data Type | Size (in Bytes) | Range |
|---|---||
| short | 2 | -32,768 to 32,767 |
| unsigned short | 2 | 0 to 65,365 |
| int | 4 | -2,147,483,648 to 2,147,483,647 |
| unsigned int | 4 | 0 to 4,294,987,295 |
| long | 4 | -2,147,483,648 to 2,147,483,647 |
| unsigned long | 4 | 0 to 4,294,987,295 |