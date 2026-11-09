
### LISTING 17.4 Continued

```idl
uuid(E8482A01-A2F6-1D12-A512-00600893FB20),
helpstring("MTSOrder Class"),
TRANSACTION_REQUIRED
]
coclass MTSOrder
{
    [default] interface IMTSOrder;
};
```

## Completing Transactions

Transactional components must explicitly commit or abort an outstanding transaction. Failing to do so leaves the transaction up in the air, in which case it will commit if the object is released by the client within the transaction timeout. If the object is not released and the transaction times out, then the transaction is aborted. Leaving things to chance is hardly appropriate behavior for a mission-critical server component, and for this reason all correctly designed transactional components explicitly commit or abort their transactions. Keep in mind that all objects involved in a transaction are deactivated at the completion of the transaction. Transactions are managed through an object’s ObjectContext.

## ObjectContext

Every COM+ object has an ObjectContext associated with it. The ObjectContext maintains the implicit COM+ state information associated with the object. Of particular interest here is the fact that the ObjectContext tracks information related to the current transaction, if any exists. A COM+ object can manipulate its ObjectContext by calling the COM+ API function GetObjectContext(), which returns an IObjectContext interface pointer.

An object’s ObjectContext should never be accessed in the object’s constructor or destructor, or during any IUnknown method call. In general, this is because COM+ has either not created the context or has already destroyed it during these object calls. It is important to note that calling an object’s IUnknown method does not activate the ObjectContext. ObjectContext references (interface pointers to IObjectContext) should never be passed to other objects as they are generally invalid outside the owning object.

## IObjectContext Revisited

Listing 17.5 is an example of the one and only method for the transactional OrderEntry object.

### LISTING 17.5 PlaceOrder Method for the OrderEntry Object

```cpp
STDMETHODIMP CMTSOrder::PlaceOrder(    long AccountNumber,
                                      long ProductID,
                                      long Quantity)
{
    //Ensure that we have a transaction
    if ( ! m_spObjectContext->IsInTransaction() )
        return CONTEXT_E_TMNOTAVAILABLE;

    //Disable commit to keep an accidental
    // return in the body of our code from
    // committing the transaction on client
    // object shutdown
    m_spObjectContext->DisableCommit();

    //Compute total price and deduct account balance within
    // the current transaction (all sweaters are $20)
    double lfTotalPrice = Quantity * 20.0;
    HRESULT hr = ChargeAccount( AccountNumber, lfTotalPrice );
    if ( FAILED(hr) )
    {
        //Abort transaction and return error
        m_spObjectContext->SetAbort();
        return hr;
    }

    //Reduce our inventory within the current transaction
    hr = ReduceInventory( Quantity );
    if ( FAILED(hr) )
    {
        //Abort transaction and return error
        m_spObjectContext->SetAbort();
        return hr;
    }

    //Commit transaction and return success
    m_spObjectContext->SetComplete();
    return S_OK;
}
```

There are several points of interest in this code. The most important of which is the fact that, aside from some sanity checking and defensive programming at the top of the routine, and the SetComplete() or SetAbort() calls tied to the returns, the code is devoid of cryptic transaction instructions. Note that the two routines ChargeAccount() and ReduceInventory() could actually modify a database or create a new component and have it do so. It matters little because the transaction automatically propagates to any new objects or resource managers that support transactions. The complete example on

## Travel Agency Example

It's time to take a look at an example that models the travel agency example given early in the chapter. I've created a component with a class named `CSubmitOrder` (seen in Listing 17.6). The class checks to see if the hotel, airline, and car reservations are okay, and then writes the information to a database.

A Visual Basic program (in Listing 17.7) is the client application that uses the component.

After the code listings, there is an explanation.

### LISTING 17.6 The CSubmitOrder Class Acts on Behalf of the Travel Agent

```cpp
// CSubmitOrder.cpp: Implementation of CSubmitOrder
#include "stdafx.h"
#include "Travel.h"
#include "SubmitOrder.h"

#include "dboAirlineReservations.h"
#include "dboCarReservations.h"
#include "dboHotelReservations.h"

///////////////////////////////////////////////////////////////
// CSubmitOrder

STDMETHODIMP CSubmitOrder::DoIt()
{
    AFX_MANAGE_STATE(AfxGetStaticModuleState());

    // Get the object context.
    IObjectContext *pObjectContext = NULL;
    HRESULT hRes = GetObjectContext( &pObjectContext );

    // Make sure we didn't get an error while getting
    // the object context.
    if( FAILED( hRes ) )
    {
        if( hRes == E_INVALIDARG )
            m_strStatus = "Invalid argument.";
        else if( hRes == E_UNEXPECTED )
            m_strStatus = "Unexpected error.";
        else if( hRes == CONTEXT_E_NOCONTEXT )
            m_strStatus = "No context associated with object.";
        else
            m_strStatus = "Object context could not be obtained.";

        return( hRes );
    }

    // Check and store the hotel information below.
    CdboHotelReservations Hotel;

    // Check to make sure the hotel reservations are valid.
    if( !HotelReservationOK() )
    {
        m_strStatus = "Problem with hotel reservations.";
        pObjectContext->SetAbort();
        return( S_OK );
    }

    // Attempt to open the Hotel table.
    hRes = Hotel.Open();
    if( FAILED( hRes ) )
    {
        m_strStatus = "Hotel did not open.";
        pObjectContext->SetAbort();
        return( hRes );
    }

    // Store the information into the Hotel
    // class and then update the database.
    strcpy( Hotel.m_Date, m_strStartDate );
    strcpy( Hotel.m_Type, m_strHotelType );
    strcpy( Hotel.m_Name, m_strCustomerName );
    Hotel.SetData();
    Hotel.Insert();


    // Check and store the car information below.
    CdboCarReservations Car;

    // Check to make sure the Car reservations are valid.
    if( !CarReservationOK() )
    {
        m_strStatus = "Problem with Car reservations.";
        pObjectContext->SetAbort();
        return( S_OK );
    }

    // Attempt to open the Car table.
    hRes = Car.Open();
    if( FAILED( hRes ) )
    {
        m_strStatus = "Car did not open.";
        pObjectContext->SetAbort();
        return( hRes );
    }

    // Store the information into the Car
    // class and then update the database.
    strcpy( Car.m_Date, m_strStartDate );
    strcpy( Car.m_Type, m_strCarType );
    strcpy( Car.m_Name, m_strCustomerName );
    Car.SetData();
    Car.Insert();

    // Check and store the airline information below.
    CdboAirlineReservations Airline;

    // Check to make sure the Airline reservations are valid.
    if ( !AirlineReservationOK() )
    {
        m_strStatus = "Problem with Airline reservations.";
        pObjectContext->SetAbort();
        return( S_OK );
    }

    // Attempt to open the Airline table.
    hRes = Airline.Open();
    if( FAILED( hRes ) )
    {
        m_strStatus = "Airline did not open.";
        pObjectContext->SetAbort();
        return( hRes );
    }

    // Store the information into the Airline
    // class and then update the database.
    strcpy( Airline.m_Date, m_strStartDate );
    strcpy( Airline.m_Type, m_strAirlineType );
    strcpy( Airline.m_Name, m_strCustomerName );
    Airline.SetData();
    Airline.Insert();

    m_strStatus = "Transaction completed.";

    // Commit the transaction.
    pObjectContext->SetComplete();

    // Release the object context.
    pObjectContext->Release();

    return S_OK;
}
```
