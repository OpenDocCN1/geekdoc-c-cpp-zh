When a valid character is reached, the state turns to TKS_INTEXT, which means we are now reading actual characters. When a delimiter is reached, a token is created, categorized into a type, and added to the token list. On the other hand, if a quote is encountered, our state suddenly changes to TKS_INQUOTES, which means we are now reading in a text group. As soon as another quote is encountered, the text group ends and is finalized as a string token. The same process happens for single- and multi-line comments.

The main function to examine is TokenizeString(). This is where the characters are sequentially iterated over, and states change based on character conditions. The token classification is done through the function ClassifyToken() (Listing 1.2.3), which basically determines whether it matches the characteristics of a float, a special character (from the special character table), or a string. This function is actually a prime candidate for being recursive, but this has been skipped for illustrative purposes. As you can see, it identifies whether a string can be converted to a digit, and if so, whether it is negative. Isdigit() is used to determine whether the string is a number, but by comparison, it would be just as easy to scan the string for a period (denoting a fractional number). IsSpecialCharacter() merely checks the first character of the string to see if it is a one-character special token like an open brace, bracket, or quote. If you were to add a semicolon as a token type, for instance, this would be the place to check for it. When a token is ready to be made, the classified token is created with the AllocToken() function. If the tokenization ends prematurely, the FinalizeToken() function is called, which makes sure no token is left behind. After we have a token list, it is time to parse through it, but what exactly are we parsing? First we must create some kind of text format. Let's quickly examine something called the BN Form, shown in Listing 1.2.3.

# Listing 1.2.3 Implementation of ClassifyToken() (Comments Removed for Clarity)

```
TOKENTYPE CTokenizer::ClassifyToken( const char *strText,
                                     unsigned long uIFlags )
{
    TOKENTYPE TokenType;

    if ( !( uIFlags & TKFLAG_STRINGSONLY ) && ( isdigit( strText[ 0 ]
        || ( strlen( strText ) >>= 2 && ( strText[ 0 ] == '-' && isdigit(
        strText[ 1 ] ) ) ) ) )
    {
        return TK_FLOAT;
    }
    else if ( TokenType = IsSpecialCharacter( strText[ 0 ] ) )
    {
        return TokenType;
    }
    else
    {
        return TK_STRING;
    }
}
```