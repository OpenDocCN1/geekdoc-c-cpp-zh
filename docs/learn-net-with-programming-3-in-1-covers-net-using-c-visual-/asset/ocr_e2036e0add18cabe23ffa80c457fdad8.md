```
Public static int Main(String[] args)
{
	Streamwriter writer = null;
	If (args.Length < 2)
	{
		Console.writeline(usagetext);
		Return 1;
	}
	Try
	{
		Write = new strmwriter(args[1]);
		Console.setout(writer);
		Console.setin(new streamreader(args[0]));
	}
	Catch(ioexception e)
	{
		Textwriter errorwriter = Console.Error;
		Errorwriter.writeline(e.Message);
	}
}
```