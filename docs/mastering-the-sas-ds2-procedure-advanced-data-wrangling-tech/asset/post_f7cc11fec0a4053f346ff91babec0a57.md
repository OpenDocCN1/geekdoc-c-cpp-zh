
## Figure 5.5: Report Produced Using Hash Iterator Lookup Techniques Lowest and Higest Cost Products

| Product_ID | ProductName | Ranking | UnitSalesPrice |
|---|---|---|---|
| 24010100232 | Dartsharper Key ring | Lowest Cost | 4.16 |
| 24010100031 | Capsy Hood | Second Lowest Cost | 4.81 |
| 23010700009 | Family Holiday 6 | Second Highest Cost | 738.53 |
| 24030100032 | Letour Trimag Bike | Highest Cost | 819.52 |

## 5.4 The HTTP and JSON Packages

### 5.4.1 General

For years I've used the FILENAME URL statement to access data from- Internet-based application programming interfaces (APIs) in SAS. The data returned by an API was JavaScript Object Notation (JSON) format. As a format for data interchange, JSON is both easy for machines to parse and generate and easy for humans to read and write. It is based a subset of the JavaScript programming language and uses JavaScript syntax for describing data. SAS has had PROC JSON for quite some time, but it only writes JSON files, it don't read them. Without SAS tools for parsing JSON, I became quite adept at writing DATA steps with complex string manipulation routines that provide the data I need from tags.

When DS2 launched without any raw data tools, I was disappointed to think that I would not be able to access Internet APIs from DS2. I shouldn't have been pessimistic! The SAS 9.4 ME Release in 2014 brought us the HTTP package, and I was back in bringing Internet APIs. By my absolute delight, in July of 2015 the SAS 9.4 M delivered the JSON package, and for the first time SAS had a native tool for both reading and parsing JSON.

We'll be using the API from Kiva.org for demo code. Kiva is a nonprofit organization with a mission to connect people to alleviate poverty throughout the world. Through their website (http://kiva.org), Kiva connects individuals to entrepreneurs in developing nations using a worldwide network of microfinance institutions. Individuals make small loans of $25 each. These funds are aggregated and then microfinance institutions manage all of the loans. This financing for very small businesses that would not normally have access to loans, opening up tremendous opportunity for our loan recipients. Fortunately for us, Kiva also provides an extensive API with excellent documentation provided at http://build.kiva.org, which we will use in our DS2 code examples. We will use the Kiva API to gather information about loans by female entrepreneurs in South America.

Note: Here's a little background about how I came to the HTTP and JSON package examples used in this book, and why I chose Kiva for the demo code in this book. As the son of Baptist missionaries, I was raised in northern Brazil. I came to the US to make up lost residency when I was 15 years old. Decades later, my ability to speak both Portuguese and English landed my first job with SAS, first working in Brazil, then in the Andean region of South America and the Caribbean. I eventually migrated to a post with SAS in the United States, but I still have many friends and contacts in South America. So I feel a deep connection with the people of that region, particularly for those struggling to lift themselves from extreme poverty. My research indicates that giving women a hand up is an excellent strategy for the standard of living in lives, I'm interested in making loans to female-owned businesses in South America.

### 5.4.2 HTTP Package Specifications

The HTTP package allows you to construct an HTTP client, create an HTTP GET, HEAD, or POST method and execute those methods to retrieve or post data via the Internet. You can retrieve the response information from the web server as a complete entity or you can stream the response. With the HTTP package you can also retrieve status codes from HTTP responses, socket time-values, and log the HTTP traffic between the HTTP client and server using the SAS logging facility.

### 5.4.2.1 Understanding the GET, HEAD, and POST Methods

Most APIs on the Internet consist of a collection of methods properly formed Uniform Resource Identifiers (URIs). The API will have a base URL to which additional information is appended. To access the desired API method, specify the desired response format and pass in the parameters required by the method.

The API calls can be for GET, HEAD, or POST methods.

- The GET method is used to retrieve information from the server. GET requests are used only to retrieve data, and should have no effect on the server's data.
- The HEAD method works just like GET, but a HEAD request will return only the status and header information given the request without returning the detailed data (body) of the request.
- POST methods are used to send data to the server. POST requests are generally used to upload data or to update data on the server.

Our examples will focus on using the GET method to retrieve information from an API method call.

### 5.4.2.2 Working with the Kiva API

All calls to the Kiva API will use the GET method. The Kiva API base URL is http://api.kivars.org/v1/. For example, to get a list of microfinance partners in HTML, the URI would be http://api.kivars.org/v1/partners.html. Typing that URI into a browser produces a result like:

## Figure 5.6: HTML Output results

| id | name | status | start_date | delinquency_rate | default_rate | total_amount_raised | loans_posted | portfolio_yield |
|---|---|---|---|---|---|---|---|---|
| 1 | East Africa Beta | closed | 2006-04-09 15:17:00 | 0 | 9.191729323083 | 26600 | 62 | |
| 2 | The Shush | closed | 2006-04-02 15:17:00 | 0 | 57.157727272727 | 4400 | 15 | |
| 3 | Regional Development Ca | closed | 2006-02-03 15:18:00 | 0 | 14.456040817935 | 36700 | 44 | |
| 4 | Savings Coverage Microfinance | closed | 2006-03-29 15:18:00 | 0 | 5.1297209219858 | 36250 | |
| 5 | Prisma Microfinance | closed | 2006-03-29 15:18:00 | 0 | 39925 | |

Typing that URI into a browser produces a result like (other browsers might require you to download the file and view it in another program):

## Figure 5.7: JSON Output from Kiva API Call

```json
{
  "id": 1,
  "total": 397,
  "page": 100,
  "partners": [
    {
      "id": "1",
      "name": "East Africa Beta",
      "status": "closed",
      "start_date": "2006-04-09T15:17:00Z",
      "delinquency_rate": 0,
      "default_rate": 9.191729323083,
      "total_amount_raised": 26600,
      "loans_posted": 62,
      "portfolio_yield": null,
      "href": "http://www.google.com",
      "interest": true,
      "average_loan_size_capita": 600,
      "at_risk_rate": 0,
      "currency_exchange_rate": 0,
      "currency_loss_rate": 0,
      "country": "Africa",
      "type": "loan",
      "region": "Africa"
    },
    {
      "id": "2",
      "name": "The Shush",
      "status": "closed",
      "start_date": "2006-04-02T15:17:00Z",
      "delinquency_rate": 0,
      "default_rate": 57.157727272727,
      "total_amount_raised": 4400,
      "loans_posted": 15,
      "portfolio_yield": null,
      "href": "http://www.google.com",
      "interest": true,
      "average_loan_size_capita": 600,
      "at_risk_rate": 0,
      "currency_exchange_rate": 0,
      "currency_loss_rate": 0,
      "country": "Africa",
      "type": "loan",
      "region": "Africa"
    },
    {
      "id": "3",
      "name": "Regional Development Ca",
      "status": "closed",
      "start_date": "2006-02-03T15:18:00Z",
      "delinquency_rate": 0,
      "default_rate": 14.456040817935,
      "total_amount_raised": 36700,
      "loans_posted": 44,
      "portfolio_yield": null,
      "href": "http://www.google.com",
      "interest": true,
      "average_loan_size_capita": 600,
      "at_risk_rate": 0,
      "currency_exchange_rate": 0,
      "currency_loss_rate": 0,
      "country": "Africa",
      "type": "loan",
      "region": "Africa"
    },
    {
      "id": "4",
      "name": "Savings Coverage Microfinance",
      "status": "closed",
      "start_date": "2006-03-29T15:18:00Z",
      "delinquency_rate": 0,
      "default_rate": 5.1297209219858,
      "total_amount_raised": 36250,
      "loans_posted": null,
      "portfolio_yield": null,
      "href": "http://www.google.com",
      "interest": true,
      "average_loan_size_capita": 600,
      "at_risk_rate": 0,
      "currency_exchange_rate": 0,
      "currency_loss_rate": 0,
      "country": "Africa",
      "type": "loan",
      "region": "Africa"
    },
    {
      "id": "5",
      "name": "Prisma Microfinance",
      "status": "closed",
      "start_date": "2006-03-29T15:18:00Z",
      "delinquency_rate": 0,
      "default_rate": 39925,
      "total_amount_raised": null,
      "loans_posted": null,
      "portfolio_yield": null,
      "href": "http://www.google.com",
      "interest": true,
      "average_loan_size_capita": 600,
      "at_risk_rate": 0,
      "currency_exchange_rate": 0,
      "currency_loss_rate": 0,
      "country": "Africa",
      "type": "loan",
      "region": "Africa"
    }
  ]
}
```

We will be able to search as JSON, and such API calls can generate query parameters. The parameter string follows the URI for the API method and is delimited by a question mark (?). Parameter-value pairs follow, separated by ampersands (&). For example, to use the Kiva api and request HTML results for loans from South America to females who are currently fundraising, and to return the results in descending order, with five results per page, here is the properly formed URI: http://api.aws.org/search.html?region=sa&gender=female&status=fundraising&sort=newest&page=5

### 5.4.2.3 Using the HTTP Package with the Kiva API

To use the HTTP package, we must first declare an instance of the package. We'll also declare some variables to handle the response body and return code when we execute the GET request:

```go
package http
var varchar(1000000) character set utf8 API_Response;
int rc;
```
