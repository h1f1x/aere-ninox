# Ninox API Reference - Complete Guide

The REST API supports Ninox Cloud environments and enables integration with tools like Zapier or Make.

## Table of Contents

1. [API Introduction](#api-introduction)
2. [Public Cloud API Endpoints](#public-cloud-api-endpoints)
3. [Private Cloud/On-Premises API Endpoints](#private-cloud-on-premises-api-endpoints)
4. [API Calls in Ninox Script](#api-calls-in-ninox-script)
5. [Tables, Fields and Records](#tables-fields-and-records)
6. [Integrations](#integrations)

---

## API Introduction

### Understanding and Setting Up the Ninox API

The Ninox API allows you to programmatically interact with your Ninox databases, enabling powerful integrations and automations.

### Important Notes
- Ninox has moved from ninoxdb.de to ninox.com
- Current API interface: `api.ninox.com/v1`
- It's recommended to update all integrations to use the new endpoints

### Authentication
The API uses token-based authentication. You'll need to:
1. Generate an API token from your Ninox account
2. Include the token in the Authorization header of your requests

### API Base URLs
- **Public Cloud**: `https://api.ninox.com/v1`
- **Private Cloud/On-Premises**: `https://your-instance.ninox.com/v1`

---

## Public Cloud API Endpoints

### Base URL
```
https://api.ninox.com/v1
```

### Authentication Endpoints

#### Get API Token
```http
POST /teams/{teamId}/databases/{databaseId}/tokens
```

### Team Endpoints

#### List Teams
```http
GET /teams
```

#### Get Team Details
```http
GET /teams/{teamId}
```

### Database Endpoints

#### List Databases
```http
GET /teams/{teamId}/databases
```

#### Get Database Details
```http
GET /teams/{teamId}/databases/{databaseId}
```

#### Get Database Schema
```http
GET /teams/{teamId}/databases/{databaseId}/schema
```

### Table Endpoints

#### List Tables
```http
GET /teams/{teamId}/databases/{databaseId}/tables
```

#### Get Table Details
```http
GET /teams/{teamId}/databases/{databaseId}/tables/{tableId}
```

#### Get Table Schema
```http
GET /teams/{teamId}/databases/{databaseId}/tables/{tableId}/schema
```

### Record Endpoints

#### List Records
```http
GET /teams/{teamId}/databases/{databaseId}/tables/{tableId}/records
```

Parameters:
- `filters`: Filter records based on conditions
- `order`: Sort records by field
- `page`: Page number for pagination
- `perPage`: Number of records per page

#### Get Record
```http
GET /teams/{teamId}/databases/{databaseId}/tables/{tableId}/records/{recordId}
```

#### Create Record
```http
POST /teams/{teamId}/databases/{databaseId}/tables/{tableId}/records
```

#### Update Record
```http
PUT /teams/{teamId}/databases/{databaseId}/tables/{tableId}/records/{recordId}
```

#### Delete Record
```http
DELETE /teams/{teamId}/databases/{databaseId}/tables/{tableId}/records/{recordId}
```

### File Endpoints

#### Upload File
```http
POST /teams/{teamId}/databases/{databaseId}/files
```

#### Download File
```http
GET /teams/{teamId}/databases/{databaseId}/files/{fileId}
```

### Query Endpoints

#### Execute Query
```http
POST /teams/{teamId}/databases/{databaseId}/query
```

---

## Private Cloud/On-Premises API Endpoints

### Base URL
```
https://your-instance.ninox.com/v1
```

### Key Differences from Public Cloud
- Uses your private instance domain
- May have additional security configurations
- Some endpoints might have extended functionality

### Authentication
Similar to Public Cloud but may use different authentication methods:
- API tokens
- OAuth integration
- Custom authentication schemes

### Available Endpoints
All Public Cloud endpoints are available with the same structure, using your private instance base URL.

### Example Endpoints

#### Get Database Info
```http
GET /teams/{teamId}/databases/{databaseId}
```

#### Query Records with Filters
```http
GET /teams/{teamId}/databases/{databaseId}/tables/{tableId}/records?filters=Status%3D'Active'
```

#### Bulk Operations
```http
POST /teams/{teamId}/databases/{databaseId}/tables/{tableId}/records/bulk
```

---

## API Calls in Ninox Script

### Using the http() Function

Call the Ninox API using the `http()` function in the formula editor to interact with other internet services and the Ninox API itself.

### Basic HTTP Request Structure
```javascript
http(method, url, headers, body)
```

### Authentication Headers
```javascript
let headers := {
    "Authorization": "Bearer " + apiToken,
    "Content-Type": "application/json"
};
```

### Examples

#### Get Records from Another Database
```javascript
let response := http("GET", 
    "https://api.ninox.com/v1/teams/123/databases/456/tables/Orders/records",
    {
        "Authorization": "Bearer " + ApiToken
    },
    ""
);

let records := parseJSON(response.body);
```

#### Create a New Record
```javascript
let newRecord := {
    "fields": {
        "Name": "New Customer",
        "Email": "customer@example.com",
        "Status": "Active"
    }
};

let response := http("POST",
    "https://api.ninox.com/v1/teams/123/databases/456/tables/Customers/records",
    {
        "Authorization": "Bearer " + ApiToken,
        "Content-Type": "application/json"
    },
    formatJSON(newRecord)
);
```

#### Update Existing Record
```javascript
let updateData := {
    "fields": {
        "Status": "Completed",
        "CompletedDate": now()
    }
};

let response := http("PUT",
    "https://api.ninox.com/v1/teams/123/databases/456/tables/Orders/records/789",
    {
        "Authorization": "Bearer " + ApiToken,
        "Content-Type": "application/json"
    },
    formatJSON(updateData)
);
```

#### Delete Record
```javascript
let response := http("DELETE",
    "https://api.ninox.com/v1/teams/123/databases/456/tables/Orders/records/789",
    {
        "Authorization": "Bearer " + ApiToken
    },
    ""
);
```

### Error Handling
```javascript
let response := http("GET", url, headers, "");

if response.status = 200 then
    let data := parseJSON(response.body);
    // Process successful response
    data
else
    // Handle error
    alert("API Error: " + response.status + " - " + response.body);
    null
end
```

### Pagination Handling
```javascript
function getAllRecords(tableUrl) do
    let allRecords := [];
    let page := 1;
    let hasMore := true;
    
    while hasMore do
        let response := http("GET", 
            tableUrl + "?page=" + page + "&perPage=100",
            {"Authorization": "Bearer " + ApiToken},
            ""
        );
        
        if response.status = 200 then
            let data := parseJSON(response.body);
            allRecords := array(allRecords, data.records);
            hasMore := count(data.records) = 100;  // Check if more pages exist
            page := page + 1;
        else
            hasMore := false;
        end
    end;
    
    allRecords
end
```

---

## Tables, Fields and Records

### Query Parameters for Record Retrieval

When retrieving data for tables using GET, POST, PUT, or DELETE requests, you can use various query parameters:

#### Filtering
```http
GET /tables/{tableId}/records?filters=Status='Active'
```

Common filter operators:
- `=` - Equal to
- `!=` - Not equal to  
- `>` - Greater than
- `<` - Less than
- `>=` - Greater than or equal
- `<=` - Less than or equal
- `contains()` - Contains text
- `startsWith()` - Starts with text

#### Sorting
```http
GET /tables/{tableId}/records?order=Name
GET /tables/{tableId}/records?order=CreatedDate desc
```

#### Pagination
```http
GET /tables/{tableId}/records?page=2&perPage=50
```

### Field Types and API Representation

#### Text Fields
```json
{
    "Name": "Customer Name",
    "Description": "Customer description"
}
```

#### Number Fields
```json
{
    "Amount": 1250.75,
    "Quantity": 5
}
```

#### Date Fields
```json
{
    "CreatedDate": "2023-12-01T10:30:00Z",
    "DueDate": "2023-12-15"
}
```

#### Choice Fields
```json
{
    "Status": "Active",
    "Priority": "High"
}
```

#### Multi-Choice Fields
```json
{
    "Categories": ["Category1", "Category2", "Category3"]
}
```

#### Related Records
```json
{
    "Customer": {
        "id": 123,
        "Name": "Customer Name"
    }
}
```

### Record Structure
```json
{
    "id": 123,
    "sequence": 1,
    "createdAt": "2023-12-01T10:30:00Z",
    "createdBy": {
        "id": 456,
        "name": "User Name"
    },
    "modifiedAt": "2023-12-01T15:45:00Z",
    "modifiedBy": {
        "id": 456,
        "name": "User Name"
    },
    "fields": {
        "Name": "Record Name",
        "Status": "Active",
        // ... other fields
    }
}
```

---

## Integrations

### Connecting Ninox with External Software Solutions

Using integrations, you can create connections between Ninox and other applications.

### Supported Integration Platforms

#### Zapier
- Pre-built Ninox connector available
- Supports triggers and actions
- Easy setup with GUI interface

#### Make (formerly Integromat)
- Advanced integration scenarios
- Complex data transformations
- Multiple API calls in single scenario

#### Custom Integrations
- Direct API usage
- Webhook support
- Custom authentication flows

### Integration Examples

#### Webhook Integration
```javascript
// Set up webhook endpoint in external system
let webhookUrl := "https://external-system.com/webhook";

// Send data to webhook
let payload := {
    "event": "record_created",
    "record": {
        "id": Id,
        "name": Name,
        "status": Status
    }
};

let response := http("POST", webhookUrl, {
    "Content-Type": "application/json"
}, formatJSON(payload));
```

#### Email Integration
```javascript
// Send data via email API service
let emailData := {
    "to": CustomerEmail,
    "subject": "Order Confirmation #" + OrderNumber,
    "html": formatOrderEmail(this)
};

http("POST", "https://api.emailservice.com/send", {
    "Authorization": "Bearer " + EmailApiToken,
    "Content-Type": "application/json"
}, formatJSON(emailData));
```

#### CRM Integration
```javascript
// Sync customer data to external CRM
let customerData := {
    "name": Name,
    "email": Email,
    "phone": Phone,
    "company": Company,
    "customFields": {
        "ninoxId": text(Id),
        "lastOrderDate": LastOrderDate
    }
};

http("POST", "https://api.crm-system.com/contacts", {
    "Authorization": "Bearer " + CrmApiToken,
    "Content-Type": "application/json"
}, formatJSON(customerData));
```

### Integration Best Practices

#### 1. Error Handling
```javascript
function safeApiCall(method, url, headers, body) do
    try
        let response := http(method, url, headers, body);
        if response.status >= 200 and response.status < 300 then
            response
        else
            alert("API Error: " + response.status);
            null
        end
    catch error
        alert("Network Error: " + error);
        null
    end
end
```

#### 2. Rate Limiting
```javascript
// Add delays between API calls to respect rate limits
sleep(1000);  // Wait 1 second between calls
```

#### 3. Data Validation
```javascript
// Validate data before sending to external APIs
if Email != null and contains(Email, "@") then
    // Send to external system
else
    alert("Invalid email address");
end
```

#### 4. Logging
```javascript
// Log integration activities
let logEntry := "API call to " + url + " at " + now();
// Store in log table or field
```

---

## Complete API Workflow Examples

### Customer Synchronization
```javascript
// Sync customers between Ninox and external CRM
function syncCustomers() do
    let customers := select Customers where ModifiedDate > LastSyncDate;
    
    for customer in customers do
        let customerData := {
            "externalId": customer.ExternalId,
            "name": customer.Name,
            "email": customer.Email,
            "phone": customer.Phone,
            "lastModified": customer.ModifiedDate
        };
        
        let response := if customer.ExternalId != null then
            // Update existing customer
            http("PUT", 
                "https://api.crm.com/customers/" + customer.ExternalId,
                authHeaders(),
                formatJSON(customerData)
            )
        else
            // Create new customer
            http("POST",
                "https://api.crm.com/customers",
                authHeaders(), 
                formatJSON(customerData)
            )
        end;
        
        if response.status >= 200 and response.status < 300 then
            let responseData := parseJSON(response.body);
            customer.ExternalId := responseData.id;
            customer.LastSyncDate := now();
        end
    end;
    
    // Update global sync timestamp
    LastSyncDate := now();
end
```

### Order Processing Workflow
```javascript
// Process order through multiple external systems
function processOrder(orderId) do
    let order := record("Orders", orderId);
    
    // 1. Create invoice in accounting system
    let invoiceResponse := http("POST",
        "https://api.accounting.com/invoices",
        authHeaders(),
        formatJSON({
            "customerId": order.Customer.ExternalId,
            "items": order.Items,
            "total": order.Total
        })
    );
    
    if invoiceResponse.status = 201 then
        order.InvoiceId := parseJSON(invoiceResponse.body).id;
        
        // 2. Update inventory system
        for item in order.Items do
            http("PUT",
                "https://api.inventory.com/products/" + item.ProductId,
                authHeaders(),
                formatJSON({
                    "quantity": item.Quantity,
                    "operation": "decrease"
                })
            );
        end;
        
        // 3. Send notification
        sendEmail(order.Customer.Email, 
            "Order Processed", 
            "Your order #" + order.Number + " has been processed."
        );
        
        order.Status := "Processed";
    else
        alert("Failed to create invoice");
    end
end
```

---

**Note**: This API reference covers all documented endpoints and integration patterns. Always refer to the latest Ninox API documentation for any updates or changes.

**Source**: Ninox Community Documentation - API Section  
**Total Articles**: 6  
**Language**: German (translated content)
