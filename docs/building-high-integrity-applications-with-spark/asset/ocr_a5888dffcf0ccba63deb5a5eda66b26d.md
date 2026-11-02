```
Write_Status  : Writer.Status_Type;
begin
  loop
    Reader.Receive (Message => Network_Request,
                    From    => Client_Address,
                    Status  => Read_Status);

    if Read_Status /= Reader.Success then
      Logger.Write_Error(" Failure reading request message!");
    else
      Request_Message := Messages.From_Network (Network_Request);
      Timestamp_Maker.Create_Timestamp (Request_Message, Response_Message);
      Network_Response := Messages.To_Network (Response_Message);

      Writer.Send (Message => Network_Response,
                   To      => Client_Address,
                   Status  => Write_Status);

      if Write_Status /= Writer.Success then
        Logger.Write_Error(" Failure sending reply message!");
      end if;
    end if;
  end loop;
end Service_Clients ;
```

The variables Network_Request and Network_Response hold raw octets of type Network.Octet received from and being sent to the network. They are records that carry a fixed size array along with a count of the number of elements in that array actually being used. The variables Request_Message and Response_Message hold raw octets of type Hermes.Octet that contain DER encoded ASN.1 data.

The functions From_Network and To_Network only do type conversions on the data from Network.Octet to Hermes.Octet and vice versa. Although it may seem pedantic to distinguish between different kinds of octets, it makes sense because data on the underlying network may have many forms. Hermes works only with DER encoded ASN.1. But in the future, time stamp messages may be encapsulated in some application protocol such as HTTP. So distinguishing between raw network data and the time stamp messages would be useful in a future version of Thumper.

The procedure Create_Timestamp converts request messages into response messages. Every request generates a response; invalid or malformed requests generate error responses. Create_Timestamp is the heart of the application and is almost purely functional. It accepts one array of octets and returns another.