```
```
<== f-3     (person (name "John Hill"))
             (address "37 Cherry Lane"))
==> f-4     (person (name "John Hill"))
             (address "37 Cherry Lane"))
==> Activation 0 process-moved-information: f-2,f-4
FIRE 3 process-moved-information: f-2,f-4
<== f-4     (person (name "John Hill"))
             (address "37 Cherry Lane"))
==> f-5     (person (name "John Hill"))
            (address "37 Cherry Lane"))
==> Activation 0 process-moved-information: f-2,f-5
CLIPS>
```
```

The program executes an infinite loop since it asserts a new person fact after modifying the fact bound to ?f2, thus reactivating the process-moved-information rule. Remember that a modify command is treated as a retract command followed by an assert command. Since the run command was told to fire only three rules, that is when the program stopped. If no limit argument had been given to the run command, the program would have looped endlessly. The only way to stop an infinite loop like this is by interrupting CLIPS using Control-C, or another appropriate interrupt command for the computer on which CLIPS is running.

# ## 7.22 SINGLE-FIELD WILDCARDS

Sometimes it is useful to test for the existence of a field within a slot without actually assigning a value to a variable. This is particularly useful for multifield slots. For example, suppose we want to print the social security number of every person with a specified last name. The following shows the deftemplate used to describe each person, a deffacts with some predefined people, and a rule to print the social security numbers of every person with a specified last name:

```
```
(deftemplate person
   (multislot name)
   (slot social-security-number))
(deffacts some-people
   (person (name John Q. Public)
           (social-security-number 483-98-9083))
   (person (name Jack R. Public)
           (social-security-number 483-98-9084)))
(defrule print-social-security-numbers
   (print-ss-numbers-for ?last-name)
   (person (name ?first-name ?middle-name
             ?last-name)
```
```