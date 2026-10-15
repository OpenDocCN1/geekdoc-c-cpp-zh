```
</assembly>
<members>
    <member name="T:DataStorage">
        <summary>
            DataStorage is used to persist and retrieve
            employee data from the files.
        </summary>
    </member>
    <member name="M:DataStorage.Store(Employee)">
        <summary>
            Save an employee object to a file
            named with the Employee name.
        </summary>
        <remarks>
            This method uses
            <seealso cref="T:System.IO.FileStream"/>
            in addition to
            <seealso cref="T:System.IO.StreamWriter"/>
        </remarks>
        <param name="employee">
            The employee to persist to a file</param>
        <date>January 1, 2000</date>
    </member>
    <member name="M:DataStorage.Load(
        System.String,System.String)">
        <summary>
            Loads up an employee object
        </summary>
        <remarks>
            This method uses
            <seealso cref="T:System.IO.FileStream"/>
            in addition to
            <seealso cref="T:System.IO.StreamReader"/>
        </remarks>
        <param name="firstName">
            The first name of the employee</param>
        <param name="lastName">
            The last name of the employee</param>
        <returns>
            The employee object corresponding to the names
        </returns>
        <date>January 1, 2000</date>*
    </member>
</members>
</doc>
```

The resultant file includes only the amount of metadata that is necessary to associate an element back to its corresponding C# declaration. This is important to note, because in general, it is necessary to use the XML output in combination with the generated assembly to produce any meaningful