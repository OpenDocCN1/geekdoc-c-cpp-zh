```
int image[NX][NY]; //The input image
void histogram (int image[NX][NY],int h[SIZE])
{
for (int i=0;i<SIZE;i++) h[i]=0;
for (int i=0;i<NX;i++)
for (int j=0;j<NY;j++)
h[image[i][j]]++;
}
void equalize (int input[NX][NY],int output[NX][NY])
{
int h[SIZE]; //The histogram
int f[SIZE]; //The transfer function
histogram (input,h); //Compute the histogram
for (int i=0;i<SIZE;i++) //Compute transfer function
{
f[i]=0;
for (int j=0;j<=i;j++) f[i] += h[j];
f[i] *= SIZE-1;
}
for (int i=0;i<NX;i++) //Apply transfer function
for (int j=0;j<NY;j++)
output[i][j] = f[input[i][j]];
}
```

# Listing 9.1. Histogram computation and equalization.

Listing 9.1 sketches the code for computing an image histogram and using it for histogram equalization. Here, images are represented for simplicity, as two-dimensional integer arrays of size NX x NY pixels, where each pixel can have 0 ... SIZE - 1 different gray values. The histogram of some input image is computed and stored in an integer array int h[SIZE]. Next, we use this histogram to construct the transfer function

$f(x) = (SIZE - 1) \sum_{i=0}^{x} h[i]$ (9.1)

that will perform the histogram equalization [Mylers and Weeks 93]. Finally, we apply this function to all pixels of the input image.

Another use of histogram equalization is in applications where we need to compare similar images taken under slightly different illuminations or with different exposure settings. By equalizing the images, direct luminance comparison is much easier to do.