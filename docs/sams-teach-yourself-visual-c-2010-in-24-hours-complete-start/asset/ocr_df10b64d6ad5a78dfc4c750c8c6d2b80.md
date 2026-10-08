Add public read-only properties for each of the fields. For the colorRepresentation, flashMode, exposureMode, lightSource, and dateTaken fields, use the following code:

```
```csharp
public ColorRepresentation ColorRepresentation
{
    get
    {
        ColorRepresentation value = Exif.ColorRepresentation.Uncalibrated;
        if (this.colorRepresentation.HasValue)
        {
            if (!String.IsNullOrWhiteSpace(Enum.GetName(typeof
                (ColorRepresentation), this.colorRepresentation)))
            {
                value = (ColorRepresentation)this.colorRepresentation;
            }
        }

        return value;
    }
}

public DateTime? DateTaken
{
    get
    {
        DateTime? result = null;
        if (!String.IsNullOrWhiteSpace(this.dateTaken))
        {
            DateTime date;
            if (DateTime.TryParse(this.dateTaken,
                DateTimeFormatInfo.InvariantInfo, DateTimeStyles.None, out date))
            {
                result = date;
            }
        }

        return result;
    }
}

public ExposureMode ExposureMode
{
    get
    {
        ExposureMode value = Exif.ExposureMode.Unknown;
        if (this.exposureMode.HasValue)
        {
            if (!String.IsNullOrWhiteSpace(Enum.GetName(typeof
                (ExposureMode), this.exposureMode)))
            {
                value = (ExposureMode)this.exposureMode;
            }
        }
```
```