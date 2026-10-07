# 90 Mastering the SAS DS2 Procedure: Advanced Data Wrangling Techniques

# 5.4.4.1 Querying the API Using the HTML Package

Using the HTML package, let's write a method that will enable flexible queries to the Kiva API to retrieve information about the newest loans. Our method will accept parameters for geographical region, loan status, gender of applicant, and the number of rows returned. We retrieve the results into the GLOBAL VARIABLE API_Response that it can easily be passed on to a JSON parsing method.

```
method Kiva(char(2) region, varchar(20) status
    varchar(6) gender, int rows);
dcl int rc;
    /* create a GET request */
h.createGetMethod(cats(
        'http://api.kivaws.org/v1/loans/search.json?region='
        '&status='
        status,
        '&gender='
        gender,
        '&per_page='
        rows,
        '&sort_by=newest'));
    /* execute the GET query to the Kiva API */
h.executeMethod();
    /* retrieve response as text, write to the log */\nh.getResponseBodyAsString(API_Response, rc);
end;
```

# 5.4.4.2 Parsing the API Response using the JSON Package

Next, let's add a method to parse the API response using the JSON package.

```
method parseLoans(varchar(1000000) json)
dcl int rc TokenType parseFlags;
dcl nchar(1024) thisVar token
dcl int rc tokenType parseFlags;
dcl nchar(1024) token;
rc = j.setParserInput(json);
if ( rc ) then do
    put 'Error rc = ' rc setParserInput failed.';
    stop;
end;
    /* Parse the JSON */
    /* RC of 0 means all went well. Otherwise, an error occurred */
    do until (token='loans')
        j.getNextToken( rc, token, tokenType, parseFlags);
        if rc then /* This must be the end */
            do
                output;
                stop;
            end;
        if tokenType=32 then
            do
                j.getNextToken( rc, token, tokenType, parseFlags);
                if tokenType=128 then j.getNextToken( rc, token
                    , tokenType, parseFlags);
                if tokenType=64 then output;
```