Finally, on line [60], the **FillCurrencyTableFrom** member function is introduced. It is declared virtual so that it can be overridden in derived classes, if necessary. The definition of this function is contained in the *XML_CurrencyExchanger.cpp* file, presented in Listing 6.3.

# **Listing 6.3** Definition of the `XML_CurrencyExchanger` class members (in *CurrencyCalc_Lib, XML_CurrencyExchanger.cpp*).

```
```cpp
#include "XML_CurrencyExchanger.h"
#include <fstream>


namespace CppBook
{


bool    XML_CurrencyExchanger::FillCurrencyTableFrom( const wstring & currencyFile )
{

        wifstream   inFile( currencyFile );

        if( ! inFile.is_open() )
                return false;             // cannot open the input file


        // Read line by line and look for patterns


        ESearchStates  state = ESearchStates::kIdle;

        // Stores currently processed line of the XML
        wstring line;

        // Stores current match and submatches of the regex
        wsmatch  match_res;

        // These will gather partial matches of the currency record
        wstring curr_code, curr_name, buy_rate_str, sell_rate_str;

        // Read params one-by-one
        while( getline( inFile, line ) )
        {

                switch( state )
                {
                        case ESearchStates::kIdle:

                                if(regex_search(line,match_res,f_curr_name_pat)&&match_res.size()>1)
                                {
                                        // Ok, a currency code was found; let’s store it
                                        // require at least one subpression
                                        curr_name = match_res[1];        // take the first sub-match

                                        // For easier processing, replace white characters
                                        replace( curr_name.begin(), curr_name.end(), L' ', L'_' );

                                        state = ESearchStates::k_Name_Processed; // change the state
                                }

                                break;
                }
        }
```
```