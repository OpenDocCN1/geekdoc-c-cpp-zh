The listHolidays pseudocode now appears as follows:

```
// Displays the dates of all holidays in a given year.
listHolidays(year: integer): void
    date = getFirstDay(year)
    while (date.isBefore(getFirstDay(year + 1)))
    {
        if (date.isHoliday())
            write (date, " is a holiday ")
        date = date.getNextDay()
    }
```

Thus, you can design an ADT by identifying data and choosing operations that are suitable to your problem. After specifying the operations, you use them to solve your problem independently of the implementation details of the ADT.

**An appointment book.** As another example of an ADT design, imagine that you want to create a computerized appointment book that spans a one-year period. Suppose that you make appointments only on the hour and half hour between 8 a.m. and 5 p.m. You want your system to store a brief notation about the nature of each appointment along with the date and time.

To solve this problem, you can define an ADT appointment book. The data items in this ADT are the appointments, where an appointment consists of a date, time, and purpose. What are the operations? Two obvious operations are

+   Make an appointment for a certain date, time, and purpose. (You will want to be careful that you do not make an appointment at an already occupied time.)

+   Cancel the appointment for a certain date and time.

In addition to these operations, it is likely that you will want to

+   Ask whether you have an appointment at a given time.

+   Get the purpose of your appointment at a given time.

Finally, ADTs typically have initialization and destruction operations that we assume but do not specify at this stage.

Thus, the ADT appointment book can have the following operations:

```
// Returns true if an appointment exists for the date and time specified,
// false otherwise.
+isAppointment(apptDate: Date, apptTime: Time): boolean
// Inserts the appointment for the date, time, and purpose specified as long as
// // it does not conflict with an existing appointment.
// Returns true if successful, false otherwise.
+makeAppointment(apptDate: Date, apptTime: Time,
apptPurpose: string): boolean
// Deletes the appointment for the date and time specified.
// Returns true if successful, false otherwise.
+cancelAppointment(apptDate: Date, apptTime: Time): boolean
// Gets the purpose of the appointment at the given date and time, if one exists.
// Otherwise returns an empty string.
+getAppointmentPurpose(apptDate: Date, apptTime: Time): string
```

You can use these ADT operations to design other operations on the appointments. For example, suppose you want to change the date or time of a particular appointment within the existing