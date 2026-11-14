
## B

- BeginExecuteReader method, 43-44
- Behavior After Applying Exception Shielding with a Replace Handler example, 74
- Behavior After Applying Exception Shielding with a Wrap Handler example, 73
- bin folder overview, 8
- blocks, choosing, 6-7

## C

- Cache data in a database backing store example, 355
- Cache data in memory using the null backing store example, 127-130
- Cache data locally in the isolated storage backing store example, 132-133
- CacheItemRemovedAndShowCacheContents routine, 128
- Caching Application Block, 121-144
  - configuring, 124-126
  - extending, 143
  - flushing vs. expiring, 123-124
  - how to use, 122-143
    - adding and retrieving from the cache, 127-130
    - adding to cache, 137-138
    - Cache data in memory using the null backing store example, 127-130
    - caching example, 127
    - contents of the cache, 130-131
    - database backing store, 134-135
    - DataCache object expired or removed cache items example, 139-140
    - encrypting cached data, 133
    - file dependency and extended time expiration, 135-136
    - isolated storage backing store, 131-133
    - loading the cache, 141-143
      - Load the cache proactively on application startup example, 141-143
      - Load the cache reactively on demand example, 141-143
    - proactive cache loading, 141
    - reactive cache loading, 141-143
    - refreshing the cache, 138-140
    - Remove and flush cached items example, 135
  - overview, 3-4
  - what it does, 123-124
- Checking filter status and adding context information to the log entry example, 111
- composite validators, 150
- configuration
  - advanced configuration scenarios, 237-242
  - configuration based technique, 216
  - configuration console, 10-11
  - configuration sources described, 235-236
  - encrypting configuration files, 243-244
  - Enterprise Library, 10-14
  - scenarios, 237-242
  - securing, 14
- ConfigurationValidatorFactory, 372
- constructor injection with Unity, 217-232
- container
  - alternative service locator or container, 232-233
  - directly accessing, 16-17
- ContainsCharactersValidator, 173
- contributors and reviewers, xxix-xx
- Create and Compare Hash Values for Data Items example, 193-195
- Create and Compare Hash Values for Text Strings example, 191-193
- CreateConnection method, 27
- Creating and Using Validators Directly example, 173
- Creating and writing log entries with a LogEntry object example, 104-105
- Credential Management
  - overview, 4
  - see also Security Application Block
- Cryptographic Key Wizard, 186
- Cryptography Application Block, 183-196
  - custom cryptography providers, 195
  - encryption keys, 184-185
  - examples, 187-195
    - Create and Compare Hash Values for Data Items example, 193-195
    - Create and Compare Hash Values for Text Strings example, 191-193
    - DecryptSymmetric method, 188
    - Encrypt and Decrypt a Text String using a Symmetric Algorithm example, 188-189
    - Encrypt and Decrypt Data using a Symmetric Algorithm example, 189-191
    - encrypting and decrypting a text string, 188-189
    - encrypting and decrypting data symmetric provider, 188
    - EncryptSymmetric method, 188
    - hash values, 191-195
    - object instances, 189-191
  - hashing, 184
  - how to use, 185-187
    - adding the required references, 187
    - configuring cryptographic providers, 186
    - integration with other blocks, 185
  - overview, 4
  - shared key encryption, 184
  - symmetric encryption, 184
  - what it does, 185

## D

- Data Access Application Block, 25-59
  - accessor creation, 37-38
  - accessors overview, 35-36
  - assemblies, 28-29
  - configuring, 28-29
  - connection-based transactions, 53-55
  - connections, 52
  - data operations supported by, 26-28
  - distributed transactions, 55-57
    - DTC transactions, 56
  - how to use, 28-57
  - methods supported by, 26-28
  - multiple rows, 33-35
    - array of parameter values, 32-33
    - named parameters, 33-35
    - query parameters, 33-35
  - other databases no parameters, 31-32
  - overview, 4
  - retrieving data as objects, 35-38
  - retrieving data asynchronously, 41-45
    - access, 42-43
    - row set data, 45
  - sample applications, 30-31
  - single scalar values, 40-41
  - updating data, 45-51
    - DataSets, 47-51
    - update queries, 46-51
    - updating the database from a DataSet, 48-51
  - what it does, 26-28
  - XML data, 39-40
- data annotation attributes approach, 157
- DataAnnotations attribute, 151-152
- Database class, 29
- Database instances, 29-30
- DataReader method, 31-32
- DataSets, 47-51
- DbTransaction type, 54
- dependency injection
  - described, xiii, 1-5, 223
  - in Enterprise Library, 227-232
  - with Unity, 223-224
- Detect and refresh expired or removed cache items example, 139-140
- DI (dependency injection) see dependency injection
- Distributed Transaction Coordinator (DTC) service, 30-31
  - transactions, 55-56
- distributed transactions, 55-57
- dynamic registration technique, 216

## E

- Encrypt and Decrypt a Text String using a Symmetric Algorithm example, 188-189
- Encrypt and Decrypt Data using a Symmetric Algorithm example, 189
- Encrypt cached data in a backing store example, 133
- EncryptedCacheManager manager, 124-125
- encryption
  - configuration, 14
  - configuration files, 243-244
  - Enterprise Library, 123
- Enterprise Symmetric method, 188
- Enterprise Library, 1-23
  - assemblies and references overview, 7-8
  - the big picture, 2
  - bin folder overview, 8
  - configuring, 10-14
  - dependency injection, 227-232
  - described, xiii, 1-15
  - example applications, 22
  - fundamentals, 6-9
  - getting objects from previous versions, 21-22
  - global assembly cache (GAC) overview, 8
  - installation, 7-9
  - installing, 7
  - instance creation, 14-22
  - instantiating objects, 14-22
  - scenario overview, 3-4
  - service locators, 16-17
  - uses, 3-5
- Enterprise Library service locator approach, 16-21
- error management see Exception Handling Application Block
- example applications, 22
- Exception Handling Application Block, 61-87
  - assisting administrators, 85-86
  - choosing exception policies, 63-67
    - about policies, 63-65
    - allowing exceptions to propagate, 63
    - choosing an exception handling strategy, 65-66
    - MyTestExceptionPolicy exception handling policy, 64-65
  - Process method, 67-68
  - Process method vs. HandleException method, 66
  - executing code, 85-84
  - extending exception handling, 87
  - how to use, 62
  - logging exceptions, 75-77
  - overriding exceptions, 74
  - shielding exceptions at WCF service boundaries
    - creating a fault contract, 78
    - editing service code, 79-80
    - exception handling policy, 78-79
    - Fault Contract exception handler, 80-81
  - shielding exceptions at WCF service boundaries, 78-81
  - simple example, 68-70
    - exception shielding, 69-70
  - specific exception types, 82
  - when to use, 62
  - wrapping exceptions, 70-73
    - configuring the wrap exception handler policy, 70
    - editing the application code to use the new policy, 71-73
    - initializing the exception handling block, 71
- Exception Logging pattern, 62
- Exception Shielding pattern, 61
- Exception Translation pattern, 62
- Execute a command that retrieves data as objects asynchronously example, 45
- Execute a command that retrieves data asynchronously example, 44-45
- ExecuteDataSet method, 27, 48-49, 51-52
- ExecuteNonQuery method, 27, 46-47
- ExecuteReader method, 27, 31
- ExecuteScalar method, 27
- ExecuteSprocAccessor method, 27
- ExecuteSqlStringAccessor method, 27
- ExecuteXmlReader method, 27
- Executing Custom Code Before and After Handling an Exception example, 83-84
- expirations
  - example, 207-208
  - table of, 136
- Expire an authenticated user example, 207-208
- ExtendedFormatTime class, 136

## F

- facades, 15
- factories, 15
- Fault Contract exception handler, 78
- Fill a DataSet and update the source data example, 49
- fluent interface, 234
- forward, xiii-xiv
- functional blocks, 3
- fundamentals, 6-9

## G

- GetInstance method, 16-17, 203
- GetParameterValue method, 27
- GetSqlStringCommand method, 27, 34
- GetStoredProcCommand method, 27, 34
- global assembly cache (GAC) overview, 8

## H

- HandleException method vs. Process method, 66
- HandlingInstanceID value, 85-86
- hash values, 192-195
- how to use this guide, xv-xvii

## I

- IHashProvider interface, 195
- Imports statement, 9
- injection
  - constructor injection with Unity, 217-232
  - dependency injection in Enterprise Library, 227-232
  - dependency injection with Unity, 213-224
  - method call injection, 222-223
  - property injection in Enterprise Library, 233-234
  - property (setter) injection, 220-221
- in-memory only example, 128-130
- installation, 7-9
- instantiation
  - instance creation, 15-21
  - of objects, 14-22
  - pros and cons of, 18-19
- interception, 233
- introduction, 1-23
- ISymmetricCryptoProvider interface, 195

## L

- Librarian, 1
- LoadDataSet method, 27
- Load the cache proactively on application startup example, 141
- Load the cache reactively on application startup example, 141-143
- Load the cache reactively on demand example, 163
- LogEntry object, 104-105
- Logging Application Block, 89-119
  - creating custom trace listeners, filters, and formatters, 119
  - how to use, 93-102
    - configuring, 93-94
    - controlling output formatting, 101-102
    - filtering by categories, 100
    - installing, 94
    - log entries to multiple categories, 100-101
    - log entry properties, 98-100
    - LogWriter example, 95-97
    - logging, 94
    - Simple logging with the Write method of a LogWriter example, 95
    - trace listeners for different categories, 99
  - importing namespaces, 9
  - logging categories, 92
  - logging overhead and additional context information, 93
  - non-formatted trace listeners, 102-118
    - adding additional context information, 113-115
    - capturing unprocessed events and logging errors, 105-107
    - Checking filter status and adding context information to the log entry example, 111
    - checking if filters will block a log entry, 112-113
    - creating and using LogEntry objects, 104-105
    - Creating and writing log entries with a LogEntry object example, 104
    - filtering all log entries by priority, 103
    - filtering by severity in a trace listener, 103
    - Sending log entries to a database example, 109
    - special sources, 105-107
    - trace sources and trace listeners, 111-112
    - Tracing activities and publishing activity information to categories example, 116-118
    - tracing and correlating activities, 115-118
    - Using special sources to capture unprocessed events or errors example, 106-107
  - overriding process diagram, 92
  - what it does, 90-93
  - Logging Filters section, 100
  - Logging handler, 75-77
  - logging to multiple categories with the write method of a log-writer example, 100-101
  - LogWriter example, 95-97

## M

- MetadataType attribute, 171-172
- Microsoft Limited Public License, 5
- MyTestExceptionPolicy exception handling policy, 64-65

## N

- namespaces, 9
- non-formatted trace listeners, 102-118

## O

- Object Collection validator, 155, 162, 165-166
- objects
  - application blocks, 15
  - getting from previous versions, 21-22
- Object validator, 155
- ObjectValidator, 155, 162, 164-165
- OrCompositeValidator, 174
