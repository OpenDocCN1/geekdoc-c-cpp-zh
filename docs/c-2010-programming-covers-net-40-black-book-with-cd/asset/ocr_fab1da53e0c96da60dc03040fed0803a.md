# Specifying Formatters

Specifying formatters means to specify the format of messages, such as binary or SOAP. These formatters are used by channels to transport messages in binary or SOAP format across network. By default, the TcpChannel class uses binary formatter and the HttpChannel class uses SOAP formatter. However, both these channels can use any one of the two formatters. The following code snippet shows how to use the SOAP formatter by the TcpChannel class:

```
IChannel chan;
IServerChannelSinkProvider SProvider;
IClientChannelSinkProvider CProvider;
...
SProvider = new BinaryServerFormatterSinkProvider();
CProvider = new BinaryClientFormatterSinkProvider();
chan = new TcpChannel(props, CProvider, SProvider);
...
ChannelServices.RegisterChannel(chan, false);
```

In the preceding code snippet, we have creates an instance of the provider that provides the formatter sink to use the formatter class to associate a formatter to a channel. The BinaryServerFormatterSinkProvider and BinaryClientFormatterSinkProvider objects provide the IServerChannelSinkProvider object and the IClientChannelSinkProvider object, respectively, which use the BinaryFormatter class to encode the message in the binary format.

After creating sink providers, you can specify a formatter, as shown in the following code snippet:

```
private void Start()
{
    try
    {
        IDictionary props = null;
        props = new Hashtable();
        props["port"] = TextBox2.Text;
        if (rbtnBinary.Checked)
        {
            SProvider = new BinaryServerFormattersSinkProvider();
            CProvider = new BinaryClientFormattersSinkProvider();
            if (cbtnFullTrust.Checked)
            {
                ((BinaryServerFormattersSinkProvider)SProvider).TypeFilterLevel = TypeFilterLevel.Full;
            }
        }
        else if (rbtnSoap.Checked)
        {
            SProvider = new SoapServerFormattersSinkProvider();
            CProvider = new SoapClientFormatterSinkProvider();
            if (cbtnFullTrust.Checked)
            {
                ((SoapServerFormattersSinkProvider)SProvider).TypeFilterLevel = TypeFilterLevel.Full;
            }
        }
        if (rbtnTcpChannel.Checked)
        {
            chan = new TcpChannel(props, CProvider, SProvider);
        }
        else if (rbtnHttpChannel.Checked)
```