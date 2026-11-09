# String methods: upcase, downcase, strip

Standardizing user input to have proper case can remove extra white space characters is often necessary to easily search the data later. For example, imagine you are designing a website for the New York Department of Motor Vehicles, and one page is for driver license application and renewals. Both the application and renewal forms ask for current address, which includes a field for two letter state abbreviation. After reviewing completed paper forms, and previous electronic data, you see that drivers enter the state in several ways including “NY”, “ny”, “Ny”, “nY”, and other similar variants. If “NY” was the desired result you could use upcase and strip to make this input consistent. Table 13-5 further describes these string methods.

| Method name | Description | Example | Result |
|---|---|---|---|
| `upcase` | Returns all uppercase characters | `"nY".upcase` | `"NY"` |
| `downcase` | Returns all lowercase characters | `"Hi".downcase` | `"hi"` |
| `capitalize` | Capitalizes first letter, lowercases remaining letters | `"wake UP".capitalize` | `"Wake up"` |
| `strip` | Removes leading and trailing whitespaces | `" Ny ".strip` | `"Ny"` |

# Inserting variables in strings with #

To insert variable values into strings shown to the user, you can use the hashtag sequence #{...}. The code between the open and closing curly braces is evaluated and inserted into the string. Unlike with escape sequences, the variable value is inserted only into strings created with double quotation marks. See the example code and result below.

Code:

```
yearofbirth = 1990
pplinroom = 20
puts 'Your year of birth is #{yearofbirth}. Is this correct?'
puts "Your year of birth is #{yearofbirth}. Is this correct?"
puts "There are #{pplinroom / 2} women in the room with the same birth year."
```