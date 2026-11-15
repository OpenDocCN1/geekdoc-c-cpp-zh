```
convertP6ToP3(fin, fout, image, imageInfo) :
  read_header(fin, fout, imageInfo)
  readAndWriteImageData(bin,out,image,width,height);
```

```
smooth(image, width, height):
  set i to 1
  set j to 1
  while(i<height-1)
    while(j<width-1)
      image[i][j] = (image[i][j-1] + image[i-1][j]
        + image[i][j+1] + image[i+1][j])/4
```

```
writeP3Image(ofstream& out, vector<vector<Pixel> > image, char
  comment[], int maxColor):
  writeHeader()
  for all rows
    for all columns
      write image[row][col]
```

```
readAndWriteImageData(ifstream& fin, ofstream& fout,
  vector<vector<Pixel> > image,
  int w, int h):
  allocate w rows of memory for image
  for all w
    allocate h columns
    for all h
      read red byte
      read green byte
      read blue byte
      convert bytes to unsigned int
      image[i][j]=pixel(red,green,blue)
```

```
writeHeader(ofstream& fout, char magicNumber[],
  char comment[], int w, int h,
  int maxPixelVal):
  output magicNumber
  output comment
  output w.h maxPixelVal
```

```
read_header(fin, fout, imageInfo) :
  read magic_num
  if(magic number is not P6) exit
  get next line of header
  do
    {
      if(next_ch == '#')
        save comment line
        get next line of header
      else
```