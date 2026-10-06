Execution result
0 is less than 1
0 is less than 3
0 is less than 5
0 is less than 7
0 is less than 8
2 is less than 3
2 is less than 5
2 is less than 7
2 is less than 8
4 is less than 5
4 is less than 7
4 is less than 8
5 is less than 7
5 is less than 8
6 is less than 7
6 is less than 8

# # Using the where Operator

The where operator is used to filter data according to given conditions. Like the select operator, the computation can be executed either on the server or client side. Listing 4-18 shows how to filter the student names length is greater than 4 characters long. Because the result is filtered on the server, only three items are transferred over the wire.

**LISTING 4-18** *A where example*

```
Code for the where example
let internal q2 = query {
  For n in db.Student.do
    where (n.Name.Length > 4)
    select n.Name
}

showResult q2

Execution result
"Brent"
"Anita"
"Cathy"
```

Although performing the filter action on the client side is not a recommended approach, especially if the resulting data set is large, I still list the sample code here in case complex filtering is needed on the client side. See Listing 4-19.