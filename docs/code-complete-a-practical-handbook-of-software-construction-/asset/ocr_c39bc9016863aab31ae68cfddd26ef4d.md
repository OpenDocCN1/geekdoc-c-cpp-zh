```
34
35 // add this employee's paycheck to total for accounting
36 totalWithholdings = totalWithholdings + withholding;
37 totalGovernmentRetirement = totalGovernmentRetirement + governmentRetirement;
38 totalRetirement = totalRetirement + companyRetirement;
39 }
40
41 SavePayRecords( totalWithholdings, totalGovernmentRetirement, totalRetirement );
```

In this example, you'll need one initial test case plus one for each of the five keywords, for a total of six. That doesn't mean that any six test cases will cover all the bases. It means that, at a minimum, six cases are required. Unless the cases are constructed carefully, they almost surely won't cover all the bases. The trick is to pay attention to the same keywords you used when counting the number of cases needed. Each keyword in the code represents something that can be either true or false; make sure you have at least one test case for each true and at least one for each false.

Here is a set of test cases that covers all the bases in this example:

| Case | Test Description | Test Data |
|------|-------------------|-----------|
| 1 | Nominal case | All boolean conditions are true |
| 2 | The initial for condition is false | numEmployees < 1 |
| 3 | The first if is false | m_employee[id].governmentRetirementWithheld >=MAX_GOVT_RETIREMENT |
| 4 | The second if is false because the first part of the and is false | not m_employee[id].WantsRetirement |
| 5 | The second if is false because the second part of the and is false | not EligibleForRetirement( m_employee[id] ) |
| 6 | The third if is false | not EligibleForPersonalRetirement( m_employee[id] ) |
| Note: This table will be extended with additional test cases throughout the chapter. |

If the routine were much more complicated than this, the number of test cases you'd have to use just to cover all the paths would increase pretty quickly. Shorter routines tend to have fewer paths to test. Boolean expressions without a lot of ands and ors have fewer variations to test. Ease of testing is another good reason to keep your routines short and your boolean expressions simple.

Now that you've created six test cases for the routine and satisfied the demands of structured basis testing, can you consider the routine to be fully tested? Probably not.