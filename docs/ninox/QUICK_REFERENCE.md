# Ninox Quick Reference - Essential Functions

## 🚀 Most Used Functions for Aere Integration

### **HTTP & API**
```javascript
// Make HTTP requests
http("GET", "https://api.example.com/data")
http("POST", "https://api.example.com/data", {json: data})

// Parse JSON response
parseJSON(response)
```

### **Record Operations**
```javascript
// Create new record
create(TableName, {Field1: value1, Field2: value2})

// Update record
update(this, {Field: newValue})

// Delete record
delete(record)

// Find records
select(TableName where Field = "value")
```

### **Data Processing**
```javascript
// String operations
upper(text)          // Convert to uppercase
lower(text)          // Convert to lowercase
contains(text, "substring")  // Check if contains
format(text, args)   // Format string

// Date operations  
now()               // Current date/time
date(year, month, day)  // Create date
format(dateValue, "yyyy-MM-dd")  // Format date

// Number operations
sum(array)          // Sum values
avg(array)          // Average
count(array)        // Count items
```

### **File Operations**
```javascript
// Import data
importFile(file, options)

// Create files
createTextFile("filename.txt", content)
createTempFile(content, "application/json")
```

### **Control Flow**
```javascript
// Conditionals
if condition then
    // code
else  
    // code
end

// Loops
for item in array do
    // process item
end

// Variables
let myVar := value
```

### **Error Handling**
```javascript
// Try-catch equivalent
try
    // risky code
catch
    // error handling  
end
```

## 📋 Common Patterns for Invoice Processing

### **1. Receive Invoice Data from Aere**
```javascript
let response := http("GET", aereApiUrl + "/extract/" + invoiceId, {
    headers: {
        "Authorization": "Bearer " + apiKey
    }
})

let invoiceData := parseJSON(response)
```

### **2. Create Invoice Record in Ninox**
```javascript
let newInvoice := create(Invoices, {
    InvoiceNumber: invoiceData.invoiceNumber,
    Date: date(invoiceData.date),
    Total: invoiceData.total,
    Vendor: invoiceData.vendor
})
```

### **3. Process Line Items**
```javascript
for item in invoiceData.items do
    create(InvoiceItems, {
        Invoice: newInvoice,
        Description: item.description,
        Quantity: item.quantity,
        Price: item.price
    })
end
```

### **4. Error Handling Pattern**
```javascript
try
    // Process invoice
    let result := processInvoice(data)
    alert("Invoice processed successfully: " + result.id)
catch
    alert("Error processing invoice: " + error())
end
```

---

*For complete function documentation, see [Functions Reference](./ninox_functions_reference.md)*
