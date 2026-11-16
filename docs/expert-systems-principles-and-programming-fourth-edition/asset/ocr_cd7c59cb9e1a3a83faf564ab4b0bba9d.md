# PROBLEMS

12.1 Write CLIPS rules to combine MYCIN certainty factors as shown in Section 12.2 for the following two cases:

```
New Certainty = (CF1 + CF2) + (CF1 * CF2)
if CF1 <= 0 and CF2 <= 0

New Certainty = (CF1 + CF2) / (1 - min {|CF1|, |CF2|})
if -1 < CF1 * CF2 < 0
```

12.2 Show how classical probability could be incorporated into CLIPS using the types of techniques demonstrated in Section 12.2. List possible advantages and disadvantages of using classical probability in rules.

12.3 Implement the Solve_Tree_and_Learn algorithm described in Section 12.3 using a procedural language such as LISP, C, or PASCAL. Test your implementation using the animal identification example.

12.4 Implement the Solve_Goal and Attempt_Rule algorithms described in Section 12.4 using a procedural language such as LISP, C, or PASCAL. Test your implementation using the wine selection example.

12.5 Modify the DATA-SOURCE get-data message-handler so it will allow only numeric input from the user. The handler should return only a non-numeric value if the word `hult` is entered during input.

12.6 Create a subclass of the DATA-SOURCE deftclass that allows the user to use a carriage return to indicate that the previous value of each sensor should be retained. For example, if the previous values for sensors 1 and 2 were 100 and 120, then the following responses:

```
What is the value for sensor 1? J
What is the value for sensor 2? 130.
```

should set the raw data value of sensor 1 to 100 and the raw data value of sensor 2 to 130. What assumptions should be made and what actions should be taken if the previous sensor value is unknown?

12.7 Modify the program so a device that has been shut off will continue to have its sensors monitored. If all sensors for the device return to a normal state, then the device should be turned back on.

12.8 The rule Sensor-In-Guard-Region will issue a warning for a sensor even if another rule is on the agenda, after which it will shut off its associated device. What change should be made to this rule to prevent it from issuing a warning if another rule in the WARNINGS module would turn off its associated device?