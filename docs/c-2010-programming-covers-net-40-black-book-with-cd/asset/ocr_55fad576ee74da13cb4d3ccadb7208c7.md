```
}
private void Start()
{
    try
    {
        IDictionary props = null;
        props = new Hashtable();
        props["port"] = TextBox2.Text;
        if (rbtnBinary.Checked)
        {
            SProvider = new BinaryServerFormatterSinkProvider();
            CProvider = new BinaryClientFormatterSinkProvider();
            if (cbtnFullTrust.Checked)
            {
                ((BinaryServerFormatterSinkProvider)SProvider).TypeFilterLevel = TypeFilterLevel.Full;
            }
        }
        else if (rbtnSoap.Checked)
        {
            SProvider = new SoapServerFormatterSinkProvider();
            CProvider = new SoapClientFormatterSinkProvider();
            if (cbtnFullTrust.Checked)
            {
                ((SoapServerFormatterSinkProvider)SProvider).TypeFilterLevel = TypeFilterLevel.Full;
            }
        }
        if (rbtnTcpChannel.Checked)
        {
            chan = new TcpChannel(props, CProvider, SProvider);
        }
        else if (rbtnHttpChannel.Checked)
        {
            chan = new HttpChannel(props, CProvider, SProvider);
        }
        ChannelServices.RegisterChannel(chan, false);
        if (rbtnWSingleCall.Checked)
        {
            RemotingConfiguration.RegisterWellKnownServiceType(
                typeof(SharedObject.SharedObject), "HiServerApp/HiServer",
                WellKnownObjectMode.SingleCall);
        }
        else if (rbtnWSingleton.Checked)
        {
            RemotingConfiguration.RegisterWellKnownServiceType(
                typeof(SharedObject.SharedObject), "HiServerApp/HiServer",
                WellKnownObjectMode.Singleton);
        }
        else if (rbtnCActivated.Checked)
        {
            RemotingConfiguration.RegisterActivatedServiceType(
                typeof(SharedObject.SharedObject));
        }
        Thd = System.Threading.Thread.CurrentThread;
        txtStatusBar.Text = "Connected";
    }
    catch (Exception ex)
    {
        txtStatusBar.Text = ex.Message;
    }
}
private void ListServices()
{
    lbServces.Items.Clear();
```