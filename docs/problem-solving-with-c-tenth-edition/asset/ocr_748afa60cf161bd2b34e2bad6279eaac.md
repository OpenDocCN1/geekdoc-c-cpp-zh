set template class. Read each name from the file, add it to the set, and then output all names in the set to generate the invitation list without duplicates.

+   10. Do Programming Project 16 from Chapter 8 except use a Racer class to store information about each race participant. The class should store the racer’s name, bib number, finishing position, and all of his or her split times as recorded by the RFID sensors. You can choose appropriate structures to store this information. Include appropriate functions to access or change the racer’s information, along with a constructor.
+   
+   Use a map to store the race data. The map should use the bib number as the key and the value should be the Racer object that corresponds to the bib number. With the map you won’t need to search for a bib number anymore, you can directly access the splits and final position based on the bib number.
+   
+   If you aren’t using C++11 or higher then don’t forget that you need a space between the >> characters when defining the map of vectors.

+   11. Write a program that runs a counter in a separate thread. The counter should start at one and increment its value every second. Every five seconds the counter should output its value to the console. The following line of C++11 code will make the current thread wait for one second. You will need to include `<chrono>`:
+   
+   ```cpp
+   std::this_thread::sleep_for(std::chrono::seconds(1));
+   ```
+   
+   While the counter thread is running, your main thread should allow you to input a number. If the number entered is less than or equal to the counter’s value, then the program should stop.

+   12. Write a program that uses regular expressions to validate a date in the format MM/DD/YY. YY must always be two digits, but MM could possibly be a single digit from 1 to 9 (e.g., 1 for January rather than 01) or two digits from 01 to 12. The digits in MM should not exceed 12, for example, 13 is an invalid month. Similarly, DD could also be a single digit from 1 to 9 or two digits from 01 to 31. The digits in DD should not exceed 31, for example, 32 is an invalid day. Don’t worry about months with fewer than 31 days. For example, February 31 is an invalid date but for this problem you can consider it to be valid.

+   13. Consider a freight company. This company may deliver packages around the world. Each package has a tracking code which consists of a string in the following format: destination, country code, a suburb location code which is an integer number, the character ‘C’, an integer number representing the customer id code, the character ‘W’, followed by an integer which contains the weight of the package. An example of a tracking code in this format is AU2010C42W74. Write a program which reads a tracking code in from the console and uses regex to determine if the tracking code is valid.