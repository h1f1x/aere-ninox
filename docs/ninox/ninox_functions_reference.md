# Ninox Functions Reference - Complete Guide

This comprehensive reference covers all 181+ Ninox functions organized by category.

## Table of Contents

1. [Mathematical Functions](#mathematical-functions)
2. [String Functions](#string-functions)
3. [Date and Time Functions](#date-and-time-functions)
4. [Array and Data Functions](#array-and-data-functions)
5. [UI and Navigation Functions](#ui-and-navigation-functions)
6. [File and System Functions](#file-and-system-functions)
7. [User and Security Functions](#user-and-security-functions)
8. [HTTP and API Functions](#http-and-api-functions)
9. [Database Functions](#database-functions)
10. [Utility Functions](#utility-functions)

---

## Mathematical Functions

### Basic Math
- **abs(number)** - Returns the absolute value of a number
- **ceil(number)** - Rounds a number up to the next integer
- **floor(number)** - Rounds a number down to the previous integer
- **round(number)** - Rounds a number to the nearest integer
- **sign(number)** - Returns the sign of a number (-1, 0, or 1)
- **sqr(number)** - Returns the square of a number
- **sqrt(number)** - Returns the square root of a number
- **pow(base, exponent)** - Returns base raised to the power of exponent
- **exp(number)** - Returns e raised to the power of number
- **ln(number)** - Returns the natural logarithm of a number
- **log(number)** - Returns the logarithm of a number

### Trigonometric Functions
- **sin(number)** - Returns the sine of an angle (in radians)
- **cos(number)** - Returns the cosine of an angle (in radians)
- **tan(number)** - Returns the tangent of an angle (in radians)
- **asin(number)** - Returns the arcsine of a number
- **acos(number)** - Returns the arccosine of a number
- **atan(number)** - Returns the arctangent of a number
- **atan2(y, x)** - Returns the arctangent of the quotient y/x
- **degrees(radians)** - Converts radians to degrees
- **radians(degrees)** - Converts degrees to radians

### Statistical Functions
- **avg(array)** - Returns the average of numeric values in an array
- **max(array)** - Returns the maximum value from an array
- **min(array)** - Returns the minimum value from an array
- **sum(array)** - Returns the sum of numeric values in an array
- **random()** - Returns a random number between 0 and 1
- **count(array)** / **cnt(array)** - Returns the count of elements in an array

---

## String Functions

### Basic String Operations
- **capitalize(text)** - Capitalizes the first letter of each word
- **lower(text)** - Converts text to lowercase
- **upper(text)** - Converts text to uppercase
- **trim(text)** - Removes whitespace from beginning and end of text
- **length(text)** - Returns the length of a text string

### String Manipulation
- **concat(array, separator)** - Joins array elements into a string with separator
- **join(array, separator)** - Joins array elements into a string with separator
- **split(text, separator)** - Splits text into array using separator
- **replace(text, search, replacement)** - Replaces all occurrences of search with replacement
- **substr(text, start, length)** - Extracts substring from position with length
- **substring(text, start, end)** - Extracts substring between positions

### Advanced String Functions
- **contains(text, search)** - Checks if text contains search string
- **extractx(text, regex)** - Extracts text using regular expression
- **replacex(text, regex, replacement)** - Replaces text using regular expression
- **splitx(text, regex)** - Splits text using regular expression
- **testx(text, regex)** - Tests if text matches regular expression
- **format(value, format)** - Formats value according to format string

### Text Processing
- **text(value)** - Converts value to text
- **string(value)** - Converts value to string
- **number(text)** - Converts text to number
- **numbers(text)** - Extracts numbers from text

---

## Date and Time Functions

### Current Date/Time
- **now()** - Returns current date and time
- **today()** - Returns current date
- **time()** - Returns current time

### Date Creation and Conversion
- **date(year, month, day)** - Creates date from components
- **datetime(year, month, day, hour, minute, second)** - Creates datetime from components
- **timestamp(text)** - Converts text to timestamp

### Date Components
- **year(date)** - Extracts year from date
- **month(date)** - Extracts month number from date
- **day(date)** - Extracts day from date
- **weekday(date)** - Returns weekday number
- **week(date)** - Returns week number of year
- **quarter(date)** - Returns quarter number

### Date Formatting
- **monthName(date)** - Returns month name
- **monthIndex(month)** - Returns month index
- **weekdayName(date)** - Returns weekday name
- **weekdayIndex(date)** - Returns weekday index
- **yearmonth(date)** - Returns year-month combination
- **yearquarter(date)** - Returns year-quarter combination
- **yearweek(date)** - Returns year-week combination

### Date Calculations
- **age(birthdate)** - Calculates age in years
- **days(startdate, enddate)** - Calculates days between dates
- **duration(start, end)** - Calculates duration between timestamps
- **workdays(startdate, enddate)** - Calculates working days between dates
- **endof(date, period)** - Returns end of period (month, year, etc.)
- **start(date, period)** - Returns start of period

### Time Functions
- **timeinterval(hours, minutes, seconds)** - Creates time interval
- **appointment(start, end)** - Creates appointment from timestamps

---

## Array and Data Functions

### Array Creation and Manipulation
- **array(item1, item2, ...)** - Creates array from items
- **range(start, end)** - Creates array of numbers in range
- **slice(array, start, end)** - Extracts portion of array
- **first(array)** - Returns first element of array
- **last(array)** - Returns last element of array
- **item(array, index)** - Returns item at specific index

### Array Processing
- **sort(array)** - Sorts array in ascending order
- **rsort(array)** - Sorts array in descending order
- **unique(array)** - Returns unique elements from array
- **removeItem(array, item)** - Removes item from array
- **setItem(array, index, value)** - Sets item at index to value
- **index(array, item)** - Returns index of item in array

### Data Type Functions
- **chosen(field)** - Returns selected options from multi-choice field
- **get(object, key)** - Gets value from object by key
- **set(object, key, value)** - Sets value in object by key

### Logic Functions
- **even(number)** - Returns true if number is even
- **odd(number)** - Returns true if number is odd

---

## UI and Navigation Functions

### Dialog and Alerts
- **alert(message)** - Shows alert dialog with message
- **dialog(title, message, options)** - Shows dialog with custom options

### Record Navigation
- **openRecord(record, tab)** - Opens specific record
- **closeRecord()** - Closes current record
- **closeAllRecords()** - Closes all open records
- **popupRecord(record, tab)** - Opens record in popup
- **duplicate(record)** - Duplicates current record

### Table Navigation
- **openTable(table, view)** - Opens specific table and view
- **openPage(page)** - Opens specific page
- **openFullscreen(content)** - Opens content in fullscreen
- **closeFullscreen()** - Closes fullscreen mode

### URL Functions
- **openURL(url)** - Opens URL in browser
- **url(path)** - Creates URL for Ninox path
- **urlOf(record)** - Returns URL of record
- **urlEncode(text)** - URL encodes text
- **urlDecode(text)** - URL decodes text

### Print Functions
- **printRecord(record, layout)** - Prints record with layout
- **printAndSaveRecord(record, layout)** - Prints and saves record as PDF
- **printTable(table, view)** - Prints table view
- **openPrintLayout(layout)** - Opens print layout

---

## File and System Functions

### File Operations
- **file(filename)** - Returns file attachment by name
- **files()** - Returns all file attachments
- **fileUrl(file)** - Returns URL of file
- **fileMetadata(file)** - Returns metadata of file
- **importFile(url, field)** - Imports file from URL
- **removeFile(file)** - Removes file attachment
- **renameFile(oldname, newname)** - Renames file attachment

### File Creation
- **createTempFile(content)** - Creates temporary file with content
- **appendTempFile(id, content)** - Appends content to temp file
- **createTextFile(content, filename)** - Creates text file
- **createXLSX(data, filename)** - Creates Excel file
- **createZipFile(files, filename)** - Creates ZIP file

### File Encoding
- **loadFileAsBase64(file)** - Loads file as Base64 string
- **loadFileAsBase64URL(file)** - Loads file as Base64 data URL

### Sharing Functions
- **shareFile(file)** - Shares file
- **unshareFile(file)** - Unshares file
- **shareView(view)** - Shares table view
- **unshareView(view)** - Unshares table view
- **unshareAllViews()** - Unshares all views

---

## User and Security Functions

### User Information
- **user()** - Returns current user
- **userId()** - Returns current user ID
- **userName()** - Returns current user name
- **userEmail()** - Returns current user email
- **userFirstName()** - Returns current user first name
- **userLastName()** - Returns current user last name
- **userFullName()** - Returns current user full name

### User Permissions
- **userRole()** - Returns current user role
- **userRoles()** - Returns all user roles
- **userHasRole(role)** - Checks if user has specific role
- **userIsAdmin()** - Checks if user is admin
- **users()** - Returns all users

### Security Functions
- **isAdminMode()** - Checks if in admin mode
- **isDatabaseLocked()** - Checks if database is locked
- **isDatabaseProtected()** - Checks if database is protected

---

## HTTP and API Functions

### HTTP Requests
- **http(method, url, headers, body)** - Makes HTTP request

### Data Parsing
- **parseJSON(text)** - Parses JSON string
- **formatJSON(object)** - Formats object as JSON
- **parseXML(text)** - Parses XML string
- **formatXML(object)** - Formats object as XML
- **validateXML(xml, schema)** - Validates XML against schema
- **parseCSV(text, separator)** - Parses CSV text

---

## Database Functions

### Database Information
- **databaseId()** - Returns current database ID
- **teamId()** - Returns current team ID
- **tableId(table)** - Returns table ID
- **fieldId(field)** - Returns field ID

### Record Functions
- **record(table, id)** - Returns record by table and ID

### Database Queries
- **queryConnection(query)** - Executes database query

### System Functions
- **clientLang()** - Returns client language
- **ninoxApp()** - Returns information about Ninox app
- **Ipad()** - Checks if running on iPad

---

## Utility Functions

### System Utilities
- **sleep(milliseconds)** - Pauses execution
- **waitForSync()** - Waits for synchronization
- **invalidate()** - Invalidates cache
- **cached(expression)** - Caches expression result

### Mobile Functions
- **barcodeScan()** - Scans barcode with camera
- **location()** - Gets current location
- **latitude(location)** - Extracts latitude from location
- **longitude(location)** - Extracts longitude from location

### Calendar Functions
- **createCalendarEvent(title, start, end)** - Creates calendar event
- **createCalendarReminder(title, date)** - Creates calendar reminder

### Communication
- **email(to, subject, body)** - Opens email composer
- **phone(number)** - Opens phone dialer
- **sendEmail(to, subject, body)** - Sends email
- **sendCommand(command)** - Sends system command

### Visual Functions
- **color(value)** - Returns color value
- **icon(name)** - Returns icon by name
- **styled(text, style)** - Applies styling to text
- **html(content)** - Renders HTML content
- **raw(content)** - Returns raw content

---

## Usage Examples

### Basic Examples
```javascript
// Mathematical operations
let result := abs(-5);  // Returns 5
let average := avg([1, 2, 3, 4, 5]);  // Returns 3

// String operations
let greeting := "Hello " + upper("world");  // "Hello WORLD"
let parts := split("apple,banana,orange", ",");  // ["apple", "banana", "orange"]

// Date operations
let currentAge := age(Birthdate);
let nextMonth := date(year(today()), month(today()) + 1, 1);

// Array operations
let sortedNumbers := sort([3, 1, 4, 1, 5, 9]);
let uniqueItems := unique(["a", "b", "a", "c", "b"]);
```

### Advanced Examples
```javascript
// Complex data processing
let customers := select Customers where Age > 25;
let sortedCustomers := (customers order by LastName);
let customerNames := for c in sortedCustomers do c.FirstName + " " + c.LastName end;

// File operations
let report := createTextFile(join(customerNames, "\n"), "customer_report.txt");

// API integration
let response := http("GET", "https://api.example.com/data", {}, "");
let data := parseJSON(response.body);
```

---

**Note**: This reference provides an overview of all functions. For detailed syntax and examples for specific functions, refer to the original Ninox documentation.

**Source**: Ninox Community Documentation  
**Total Functions**: 181+  
**Language**: German (translated content)
