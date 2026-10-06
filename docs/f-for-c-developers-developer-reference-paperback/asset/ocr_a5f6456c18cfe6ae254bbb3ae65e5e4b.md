# LISTING 8-7 F# worker role

```
namespace Microsoft.Samples.ServiceHosting.Thumbnails

open System
open System.Collections.Generic
open System.Collections.Configuration
open System.Diagnostics
open System.Drawing
open System.IO
open System.Text
open System.Linq
open System.Net
open Microsoft.WindowsAzure
open Microsoft.WindowsAzure.Diagnostics
open Microsoft.WindowsAzure.ServiceRuntime
open Microsoft.WindowsAzure.StorageClient

type public WorkerRole() =
    inherit RoleEntryPoint()
    [DefaultValue]
    val mutable width : int

    [DefaultValue]
    val mutable height : int

    [DefaultValue]
    val mutable configSetter : string * bool - unit

    // function to create thumbnail from a stream
    member private CreateThumbnail(input : Stream) =
    let orig = new Bitmap(input)

    if (orig.Width > orig.Height) then
        this.width <- 128
        this.height <- 128 * orig.Height / orig.Width
    else
        this.height <- 128
        this.width <- 128 * orig.Width / orig.Height

    let thumb = new Bitmap(this.width,this.height)

    use graphic = Graphics.FromImage(thumb)
    graphic.InterpolationMode <- 
        System.Drawing.Drawing2D.InterpolationMode.HighQualityBicubic
    graphic.SmoothingMode <- System.Drawing.Drawing2D.SmoothingMode.AntiAliasing
    graphic.PixelOffsetMode <- System.Drawing.Drawing2D.PixelOffsetMode.HighQuality

    graphic.DrawImage(0, 0, this.width, this.height)

    let ms = new MemoryStream()
    thumb.Save(ms,System.Drawing.Imaging.ImageFormat.jpeg)
    ms.Seek(0,SeekOrigin.Begin) |> ignore
```

CHAPTER 8 Cloud and Service Programming with F#