```
// Fig. 31.20: Reservation.java
// Airline reservation web service.
package com.deitel.reservation;

import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;
import javax.annotation.Resource;
import javax.jws.WebMethod;
import javax.jws.WebParam;
import javax.jws.WebService;
import javax.sql.DataSource;

@WebService()
public class Reservation
{
    // allow the server to inject the DataSource
    @Resource( name="jdbc/reservation" )
    DataSource dataSource;

    // a WebMethod that can reserve a seat
    @WebMethod( operationName = "reserve" )
    public boolean reserve( @WebParam( name = "seatType" ) String seatType,
        @WebParam( name = "classType" ) String classType )
    {
        Connection connection = null;
        PreparedStatement lookupSeat = null;
        PreparedStatement reserveSeat = null;

        try
        {
            connection = DriverManager.getConnection(
                DATABASE_URL, USERNAME, PASSWORD );
            lookupSeat = connection.prepareStatement(
                "SELECT \"number\" FROM \"seats\" WHERE (\"taken\" = 0) " +
                "AND (\"location\" = ?) AND (\"class\" = ?)");
            lookupSeat.setString( 1, seatType );
            lookupSeat.setString( 2, classType );
            ResultSet resultSet = lookupSeat.executeQuery();

            // if requested seat is available, reserve it
            if ( resultSet.next() )
            {
                int seat = resultSet.getInt( 1 );
                reserveSeat = connection.prepareStatement(
                    "UPDATE \"seats\" SET \"taken\"=1 WHERE \"number\"=?" );
                reserveSeat.setInt( 1, seat );
                reserveSeat.executeUpdate();
                return true;
            } // end if

```