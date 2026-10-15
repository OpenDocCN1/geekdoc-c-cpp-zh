```
</wsdl:message>
<wsdl:portType name="nmtoken">*
    <wsdl:documentation .... />?
    <wsdl:operation name="nmtoken">*
        <wsdl:documentation .... /> ?
        <wsdl:input name="nmtoken"? message="qname">?
            <wsdl:documentation .... /> ?
        </wsdl:input>
        <wsdl:output name="nmtoken"? message="qname">?
            <wsdl:documentation .... /> ?
        </wsdl:output>
        <wsdl:fault name="nmtoken" message="qname"> *
            <wsdl:documentation .... /> ?
        </wsdl:fault>
    </wsdl:operation>
</wsdl:portType>

<wsdl:binding name="nmtoken" type="qname">*
    <wsdl:documentation .... />?
    <!-- extensibility element --> *
    <wsdl:operation name="nmtoken">*
        <wsdl:documentation .... /> ?
        <!-- extensibility element --> *
        <wsdl:input> ?
            <wsdl:documentation .... /> ?
            <!-- extensibility element -->
        </wsdl:input>
        <wsdl:output> ?
            <wsdl:documentation .... /> ?
            <!-- extensibility element --> *
        </wsdl:output>
        <wsdl:fault name="nmtoken"> *
            <wsdl:documentation .... /> ?
            <!-- extensibility element --> *
        </wsdl:fault>
    </wsdl:operation>
</wsdl:binding>

<wsdl:service name="nmtoken"> *
    <wsdl:documentation .... />?>
    <wsdl:port name="nmtoken" binding="qname"> *
        <wsdl:documentation .... /> ?
        <!-- extensibility element -->
    </wsdl:port>
    <!-- extensibility element -->
</wsdl:service>
<!-- extensibility element --> *
</wsdl:definitions>
```

# Web Services Wire Format

The Web service wire format provides an interface to transmit data between a Web service and its users through protocols, such as HTTP-GET and HTTP-POST. A Web service can use any Remote Procedure Call (RPC) protocol, such as DCOM or Common Object Request Broker Architecture (CORBA), to transmit data. However, these types of protocols are not recommended for creating universally available Web services. Therefore, you need to work with frequently used protocols, such as Hypertext Transfer Protocol (HTTP) and SOAP, to transfer data between a Web service and its users.