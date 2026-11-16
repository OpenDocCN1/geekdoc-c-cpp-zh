```
String time = String.format( "%.4f ms", averagedSpeed );
g.drawString( "Area Avg", 50, textPos + 15 );
g.drawString( time, 50, textPos + 30 );

// Nearest Image
imPos = (sw + 50) * 1 + 50;
g.drawImage( nearestNeighbor, imgPos, pos, null );
time = String.format( "%.4f ms", nearestSpeed );
g.drawString( "Nearest", imgPos, textPos + 15 );
g.drawString( time, imgPos, textPos + 30 );

// Nearest2 Image
imPos = (sw + 50) * 2 + 50;
g.drawImage( nearest2, imgPos, pos, null );
time = String.format( "%.4f ms", nearest2Speed );
g.drawString( "Nearest 2", imgPos, textPos + 15 );
g.drawString( time, imgPos, textPos + 30 );

// Bilinear Image
imgPos = (sw + 50) * 3 + 50;
g.drawImage( bilinear, imgPos, pos, null );
time = String.format( "%.4f ms", bilinearSpeed );
g.drawString( "Bilinear", imgPos, textPos + 15 );
g.drawString( time, imgPos, textPos + 30 );

// Bicubic Image
imgPos = (sw + 50) * 4 + 50;
g.drawImage( bicubic, imgPos, pos, null );
time = String.format( "%.4f ms", bicubicSpeed );
g.drawString( "Bicubic", imgPos, textPos + 15 );
g.drawString( time, imgPos, textPos + 30 );

// Step Down Bilinear Image
imgPos = (sw + 50) * 5 + 50;
g.drawImage( stepDownBilinear, imgPos, pos, null );
time = String.format( "%.4f ms", stepDownBilinearSpeed );
g.drawString( "Bilin-Step", imgPos, textPos + 15 );
g.drawString( time, imgPos, textPos + 30 );

// Step Down Bicubic Image
imgPos = (sw + 50) * 6 + 50;
g.drawImage( stepDownBicubic, imgPos, pos, null );
time = String.format( "%.4f ms", stepDownBicubicSpeed );
g.drawString( "Bicub-Step", imgPos, textPos + 15 );
g.drawString( time, imgPos, textPos + 30 );
}
```