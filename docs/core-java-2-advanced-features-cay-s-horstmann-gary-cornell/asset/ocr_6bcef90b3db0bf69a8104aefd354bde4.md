# **Listing 2.1** *(Continued)*

```
~~~java
42     /*
43      * @param out a print writer
44      */
45     private static void writeData(Employee[] employees, PrintWriter out) throws IOException
46     {
47         // write number of employees
48         out.println(employees.length);
49 
50         for (Employee e : employees)
51             writeEmployee(out, e);
52     }
53 
54     /**
55      * Reads an array of employees from a scanner
56      * @param in the scanner
57      * @return the array of employees
58      */
59     private static Employee[] readData(Scanner in)
60     {
61         // retrieve the array size
62         int n = in.nextInt();
63         in.nextLine(); // consume newline
64 
65         Employee[] employees = new Employee[n];
66         for (int i = 0; i < n; i++)
67         {
68             employees[i] = readEmployee(in);
69         }
70         return employees;
71     }
72 
73     /**
74      * Writes employee data to a print writer
75      * @param out the print writer
76      */
77     public static void writeEmployee(PrintWriter out, Employee e)
78     {
79         out.println(e.getName() + "|" + e.getSalary() + "|" + e.getHireDay());
80     }
81     /**
82      * Reads employee data from a buffered reader
83      * @param in the scanner
84      */
85     public static Employee readEmployee(Scanner in)
86     {
~~~
```