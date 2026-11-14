The relative performance of integer and floating-point operations will largely be determined by the presence of a floating point unit; if one is present, integer and floating point arithmetic will probably have similar performance, otherwise, expect floating point calculations to take significantly longer (potentially by a factor of 100 or more) than integer ones. In both cases, it would seem reasonable to minimise the number of divisions wherever possible and, for integers, it may be helpful to reduce the number of multiplications as well. For any non-trivial equations, it is often a good idea to write them out by hand and some cast operations have little or no cost associated with them, but this is not always true. Casting between different integer types is fast, as is casting from a pointer to one type to a pointer to another type, because changes to the underlying data are minimal. Casting from an integer type to a floating-point type (or vice versa), however, does incur a more substantial performance penalty and the number of such casts should be kept to a minimum.

```
/* ADC offset and scaling constants. */

#define SCALE (7.5F)
#define OFFSET (2.0F)
/* A function to average 10 ADC samples. */
float average_samples(int16_t * p_adc_sample)
{
float sum = 0.0F;
/* Correct, scale and add each sample to the
* sum. */
for (int sample = 0; 10 > sample; ++sample)
{
sum += SCALE * (((float) p_adc_sample) -
OFFSET);
}
/* Divide by the number of samples (10), then
```