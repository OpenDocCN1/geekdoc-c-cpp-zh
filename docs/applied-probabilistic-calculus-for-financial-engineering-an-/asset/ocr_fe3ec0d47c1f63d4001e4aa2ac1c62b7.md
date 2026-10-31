# Arguments

+   - **instrument** — a character string giving the name of the quote symbol to download. See the webpage of the data provider for information about the available quote symbols.
+   - **start** — an R object specifying the date of the start of the period to download. This must be in a form which is recognized by `as.POSIXct`, which includes R POSIX date/time objects, objects of class `"Date"` (from package `date`) and `"chron"` and `"dates"` (from package `chron`), and character strings representing dates in ISO 8601 format. Defaults to 1992-01-02.
+   - **end** — an R object specifying the end of the download period, see above. Defaults to yesterday.
+   - **quote** — a character string or vector indicating whether to download opening, high, low, or closing quotes, or volume. For the default provider, this may be specified as `"Open"`, `"High"`, `"Low"`, `"Close"`, `"AdjClose"`, and `"Volume"`, respectively. For the provider `"oanda"`, this argument is ignored. Abbreviations are allowed.
+   - **provider** — a character string with the name of the data provider. Currently, `"yahoo"` and `"oanda"` are implemented. See http://quote.yahoo.com/ and https://www.oanda.com/ for more information.
+   - **method** — tool to be used for downloading the data. See `download.file` for the available download methods and the default settings.
+   - **origin** — an R object specifying the origin of the Julian dates, see above. Defaults to 1899-12-30 (Popular spreadsheet programs internally also use Julian dates with this origin).
+   - **compression** — Governs the granularity of the retrieved data; `"d"` for daily, `"w"` for weekly or `"m"` for monthly. Defaults to `"d"`. For the provider `"oanda"`, this argument is ignored.
+   - **retclass** — character specifying which class the return value should have; can be either `"zoo"` with `"Date"` index, or `"ts"` (with numeric index corresponding to days since `origin`).
+   - **quiet** — logical. Should status messages (if any) be suppressed?
+   - **Drop** — logical. If `TRUE` the result is coerced to the lowest possible dimension. Default is `FALSE`.