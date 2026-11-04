```
{
    if(temp > 255)
    {
        printf("Error: The value of each byte should be in [0, 255]\n");
        return 0;
    }
    bytes++;
    temp = -1; /* The value -1 means that the current address byte is checked. */
}
else
{
    printf("Error: Acceptable chars are only digits and dots\n");
    return 0;
}
else
{
    if(temp == -1)
        temp = 0; /* Make it 0, to start checking the next address byte. */
    temp = 10*temp + (ch-'0');
}
if(temp != -1) /* Check the value of the last address byte. */
{
    if(temp > 255)
    {
        printf("Error: The value of each byte should be in [0, 255]\n");
        return 0;
    }
    bytes++;
}
if(dots != 3 || bytes != 4)
    printf("Error: The IP format should be x.x.x.x\n");
else
    printf("The input address is a valid IPv4 address\n");
return 0;

```

C.9.9 Every mobile phone operating in GSM (2G) and WCDMA (3G) wireless networks is characterized by a unique identifier of 15 digits, called International Mobile Equipment Identifier (IMEI). A method to check if the device is really made by the official manufacturer is to compare the IMEI's last digit, called Luhn digit, with a check digit. If it is equal, the device is most probably authentic. Otherwise, it is not authentic for sure. The check