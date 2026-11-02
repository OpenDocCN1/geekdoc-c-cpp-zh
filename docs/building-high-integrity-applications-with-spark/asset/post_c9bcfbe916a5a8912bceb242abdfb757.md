
```ada
exception
    when Ex : Network.Socket.Network_Error =>
        Ada.Text_IO.Put_Line
            ("*** Unable to initialize network: " & Exception_Message(Ex));
end Thumper_Server;
```

The package SPARK_Boundary corresponds to the dashed box in Figure 8.4. The Service_Clients procedure executes the material inside that box in an infinite loop, making use of the (boundary) variable packages we described earlier. The specification of SPARK_Boundary is shown as follows:

```ada
pragma SPARK_Mode(On);

with Cryptographic_Services;
with Logger;
with Network.Socket.Reader;
with Network.Socket.Writer;
with Serial_Generator;

use Network.Socket;

package SPARK_Boundary is

    procedure Service_Clients
    with
        Global =>
            (Input =>
                (Reader.Input_Message_Stream, Cryptographic_Services.Key),
            In_Out =>
                (Logger.Log_Stream,
                 Writer.Output_Message_Stream,
                 Serial_Generator.State)),
        Depends =>
            (Logger.Log_Stream =>+
                (Reader.Input_Message_Stream, Writer.Output_Message_Stream,
                 Cryptographic_Services.Key, Serial_Generator.State),
             Writer.Output_Message_Stream =>+
                (Reader.Input_Message_Stream,
                 Cryptographic_Services.Key,
                 Serial_Generator.State),
             Serial_Generator.State =>+ Reader.Input_Message_Stream);

end SPARK_Boundary;
```

Notice that the with statements exactly mention those packages that are either boundary variable packages or packages containing state. These with statements are necessary so that the various abstract states can be used in the data and flow dependency contracts on Service_Clients.

The presence of the logger complicates the dependency contracts. This is unfortunate because the logger is a secondary requirement, and one might prefer that it did not clutter the essential information. Unfortunately, the SPARK tools require that flows to (and, in general from) the logger’s state be properly declared as for any other flows.

Some of the flows are surprising. In particular the dependency of the output message stream on itself. This arises because Service_Clients ultimately calls the Send procedure in the Writer package. As explained previously, this procedure might leave the output message stream unchanged. In addition if Service_Clients only gets errors when trying to receive a request, it will never even attempt to write to the output message stream. Thus the output message stream must be an In_Out global item. These details were not fully appreciated when the contracts on Service_Clients were first written. Some adjustments were made during the implementation of Service_Clients as these issues came to light.

It is interesting to note that the flow dependency contract helps with security review. Because attackers can manipulate the input message stream, any items that depend on that stream need to be carefully secured. In this case all outputs are potentially attackable. Of particular interest is the log stream. Is it possible for an attacker to send a malformed request in such a way as to cause a malformed log message to crash the server? This question is particularly interesting in light of the fact that the body of package Logger is not in SPARK. Similarly, could an attacker somehow manipulate the state of the serial number generator by sending appropriately malformed requests?

The Service_Clients procedure itself contains an infinite loop as shown:

```ada
procedure Service_Clients is
   use type Reader.Status_Type;
   use type Writer.Status_Type;

   Client_Address   : Network.Addresses.UDPv4;

   Network_Request  : Messages.Network_Message;
   Request_Message  : Messages.Message;
   Read_Status      : Reader.Status_Type;

   Response_Message : Messages.Message;
   Network_Response : Messages.Network_Message;
   Write_Status     : Writer.Status_Type;
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
end Service_Clients;
```

The variables Network_Request and Network_Response hold raw octets of type Network.Octet received from and being sent to the network. They are records that carry a fixed size array along with a count of the number of elements in that array actually being used. The variables Request_Message and Response_Message hold raw octets of type Hermes.Octet that contain DER encoded ASN.1 data.

The functions From_Network and To_Network only do type conversions on the data from Network.Octet to Hermes.Octet and vice versa. Although it may seem pedantic to distinguish between different kinds of octets, it makes sense because data on the underlying network may have many forms. Hermes works only with DER encoded ASN.1. But in the future, time stamp messages may be encapsulated in some application protocol such as HTTP. So distinguishing between raw network data and the time stamp messages would be useful in a future version of Thumper.

The procedure Create_Timestamp converts request messages into response messages. Every request generates a response; invalid or malformed requests generate error responses. Create_Timestamp is the heart of the application and is almost purely functional. It accepts one array of octets and returns another. However, because each generated time stamp is digitally signed and must include a unique serial number, Create_Timestamp needs to use the cryptographic key and the serial number generator. The SPARK declaration of Create_Timestamp is as follows:

```ada
procedure Create_Timestamp (Request_Message : in  Messages.Message;
                             Response_Message : out Messages.Message)
with
  Global =>
    (Input  => Cryptographic_Services.Key,
     In_Out => Serial_Generator.State),
  Depends =>
    (Response_Message =>
      (Request_Message, Cryptographic_Services.Key, Serial_Generator.State),
     Serial_Generator.State =>+ null);
```

The bulk of the program is actually inside Create_Timestamp. However, the high degree of purity of the procedure – it rarely references any state – means that its implementation is, in principle, straightforward. We refer you to the Thumper site on GitHub (Chapin, 2014) for the details.

## Alternate Designs

It is useful to consider some alternate designs to understand how the concepts we have developed so far apply to them. First, consider the network boundary variable packages Network.Socket.Reader and Network.Socket.Writer. These two packages encapsulate external state abstractions for input from and, respectively, output to the network. For the sake of accurate flow analysis, it is important that different state abstractions be used for inputs and outputs. Yet creating two separate packages is not strictly necessary even if two abstractions are to be used. It would be possible to define a single package with two state abstractions. Such an approach might seem more natural particularly in light of the fact that both state abstractions use a common underlying socket.

However, we anticipate that a future version of Thumper may wish to store generated time stamps for auditing. Such a change could be made by replacing the Network.Socket.Writer package body with a different body that also communicates with a database. This change would not affect the Network.Socket.Reader package at all. Two separate packages may seem like overkill, but it does clearly distinguish the inputs and outputs of the system, allowing one to be changed without interfering with the other.

The use of variable packages to hold the key and pseudorandom number generator state could also be changed. In particular, Cryptographic_Services and Serial_Generator could be converted to type packages that provided suitable
