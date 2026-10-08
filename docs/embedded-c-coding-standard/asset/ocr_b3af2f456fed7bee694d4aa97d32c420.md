```
/*!
 * @brief Compute the reflection of a set of data bits around its center.
 * @param[in] data The data bits to be reflected.
 * @param[in] num2 The number of bits.
 * @return The reflected data.
 */
static uint32_t
reflect(uint32_t data, uint8_t n_bits)
{
    uint32_t reflection = 0x00000000;

    // NOTE: For efficiency sake, n_bits is not verified to be <= 32.

    // Reflect the data about the center bit.
    //
    for (uint8_t bit = 0; bit < n_bits; ++bit)
    {
        // If the LSB bit is set, set the reflection of it.
        //
        if (data & 0x01)
        {
            reflection |= (1 << ((n_bits - 1) - bit));
        }

        data = (data >> 1);
    }

    return (reflection);
}

/* reflect() */
```