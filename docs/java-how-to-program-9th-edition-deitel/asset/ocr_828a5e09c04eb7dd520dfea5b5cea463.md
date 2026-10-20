```
47        this.seatType = seatType;
48    } // end method setSeatType
49
50    // return result
51    public String getResult()
52    {
53        return result;
54    } // end method getResult
55
56    // invoke the web service when the user clicks Reserve button
57    public void reserveSeat()
58    {
59        try
60        {
61            boolean reserved = reservationServiceProxy.reserve(
62                getSeatType(), getClassType() );
63
64            if ( reserved )
65                result = "Your reservation has been made. Thank you!";
66            else
67                result = "This type of seat is not available. " +
68                "Please modify your request and try again.";
69        } // end try
70        catch ( Exception e )
71        {
72            e.printStackTrace();
73        } // end catch
74    } // end method reserveSeat
75 } // end class ReservationBean
```

Fig. 31.22 | Page bean for seat reservation client. (Part 2 of 2.)

# 31.11 Equation Generator: Returning User-Defined Types

Most of the web services we’ve demonstrated received and returned primitive-type instances. It’s also possible to process instances of class types in a web service. These types can be passed to or returned from web service methods.

This section presents a RESTful EquationGenerator web service that generates random arithmetic equations of type Equation. The client is a math-tutoring application that accepts information about the mathematical question that the user wishes to attempt (addition, subtraction or multiplication) and the skill level of the user (1 specifies equations using numbers from 1 through 9, 2 specifies equations involving numbers from 10 through 99, and 3 specifies equations containing numbers from 100 through 999). The web service then generates an equation consisting of random numbers in the proper range. The client application receives the Equation and displays the sample question to the user.

# Defining Class Equation

We define class Equation in Fig. 31.23. All the programs in this section have a copy of this class in their corresponding package. Except for the package name, the class is identical in each project, so we show it only once. Like the TextMessage class used earlier, the server-