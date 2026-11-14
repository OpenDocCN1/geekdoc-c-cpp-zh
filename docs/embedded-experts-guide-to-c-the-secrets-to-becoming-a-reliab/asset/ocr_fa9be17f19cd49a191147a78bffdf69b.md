words), each of which is subsequently mapped to a subset of a character set that can be represented by 7-bits (typically ASCII). Thus, if the underlying data is represented as 8-bit bytes in memory, three bytes are represented as four Base64 characters. Several variations exist – there are a total of 62 alphanumeric characters in ASCII, so two additional characters must also be used, the choice of which varies for different applications; some implementations use an additional padding character when the total number of bits in the data to be encoded is not a multiple of six.

```
/* Generate a lookup table of Base64
 * encodings. */
static uint8_t const b64_table =
{
    65U, 66U, 67U, 68U, 69U, 70U,
    71U, 72U, 73U, 74U, 75U, 76U,
    77U, 78U, 79U, 80U, 81U, 82U,
    83U, 84U, 85U, 86U, 87U, 88U,
    89U, 90U, 97U, 98U, 99U, 100U,
    101U, 102U, 103U, 104U, 105U, 106U,
    107U, 108U, 109U, 110U, 111U, 112U,
    113U, 114U, 115U, 116U, 117U, 118U,
    119U, 120U, 121U, 122U, 48U, 49U,
    50U, 51U, 52U, 53U, 54U, 55U,
    56U, 57U, 43U, 47U
};
/* Encode an array of bytes in Base64. */
size_t base64_encode(uint8_t * p_in,
                     uint8_t * p_out, size_t in_size)
{
    size_t out_size;
```