# Ninox Performance Optimization Guide

This guide provides comprehensive tips and best practices for optimizing performance in Ninox applications.

## Table of Contents

1. [Best Practices Overview](#best-practices-overview)
2. [Transaction Management](#transaction-management)
3. [Script Optimization](#script-optimization)
4. [Button Performance](#button-performance)
5. [Table View Optimization](#table-view-optimization)
6. [Performance Tips and Tricks](#performance-tips-and-tricks)

---

## Best Practices Overview

The following best practices have proven to be particularly effective when working with the Ninox platform:

### Core Principles
1. **Minimize database round trips**
2. **Use appropriate transaction contexts**
3. **Optimize queries and filters**
4. **Cache expensive calculations**
5. **Avoid unnecessary data processing**

---

## Transaction Management

### Understanding Transactions

All actions within Ninox are performed as transactions. A transaction is a sequence of operations that are executed as a single unit.

### Types of Transactions

#### Reading Transactions
Used when you want to filter specific records in a table. Ninox searches the table for records that match the filter.

**Characteristics:**
- Read-only operations
- Minimal performance impact
- Safe for concurrent access

#### Writing Transactions
Used when data is changed within an action.

**Examples of writing transactions:**
- Data entry or modification
- Individual calculations
- Script execution
- Record creation/deletion

### Transaction Breaking

Ninox provides ways to break the transaction context using the `do as deferred` instruction.

**Example scenario:** When changing an invoice status should inform an external system.

```javascript
// Break transaction context
do as deferred
    // External API call that doesn't need to be transactional
    http("POST", "https://api.example.com/notify", {}, data)
end
```

### Transaction Control Commands

```javascript
// Execute within a transaction
do as transaction
    // All operations here are atomic
    create Customer;
    Name := "New Customer";
end

// Execute on server
do as server
    // Operations run server-side
    let result := heavyCalculation();
end

// Execute deferred (outside transaction)
do as deferred
    // Non-critical operations
    sendEmail("admin@company.com", "Status Update", message);
end
```

---

## Script Optimization

### Execution Context

Ninox executes scripts in constant exchange between browser/app and the server. Understanding this helps optimize performance.

### Optimization Strategies

#### 1. Minimize Server Round Trips
```javascript
// Bad: Multiple server calls
let result1 := serverFunction1();
let result2 := serverFunction2();
let result3 := serverFunction3();

// Good: Single server call with batch processing
do as server
    let result1 := serverFunction1();
    let result2 := serverFunction2();  
    let result3 := serverFunction3();
    [result1, result2, result3]  // Return results together
end
```

#### 2. Use Appropriate Transaction Context
```javascript
// For data modifications
do as transaction
    for record in records do
        record.Status := "Updated";
    end
end

// For read-only operations
do as server
    let statistics := calculateStatistics(largeDataset);
end
```

#### 3. Cache Expensive Operations
```javascript
// Use cached() for expensive calculations
let expensiveResult := cached(
    // This complex calculation will only run once
    complexCalculation(largeDataset)
);
```

#### 4. Optimize Loops
```javascript
// Bad: Process records one by one
for record in allRecords do
    record.Field := someValue;
end

// Good: Batch process with transactions
do as transaction
    for record in allRecords do
        record.Field := someValue;
    end
end
```

---

## Button Performance

### Button Execution Context

Ninox scripts triggered by buttons (or clicks on formula fields) run in the client context and not as transactions. This means Ninox executes each command separately, which can impact performance.

### Button Optimization Tips

#### 1. Use Transactions for Data Operations
```javascript
// Wrap data modifications in transactions
do as transaction
    Name := newName;
    Status := "Active";
    LastUpdated := now();
end
```

#### 2. Move Heavy Processing to Server
```javascript
// Button script
do as server
    // Heavy processing happens on server
    let results := processLargeDataset(data);
    // Update UI with results
    ProcessingResult := results;
end
```

#### 3. Provide User Feedback
```javascript
// Show progress for long operations
alert("Processing started...");
do as server
    let results := longRunningProcess();
    results
end;
alert("Processing completed!");
```

---

## Table View Optimization

Table view performance is influenced by three main factors:

### 1. Query Complexity (Filters)
- Use simple, indexed fields for filtering
- Avoid complex calculated fields in filters
- Use specific date ranges instead of open-ended queries

```javascript
// Good: Simple filter
Status = "Active"

// Less optimal: Complex calculation in filter
days(CreatedDate, today()) < 30
```

### 2. Number of Rows to Load
- Implement pagination for large datasets
- Use appropriate view limits
- Consider using summary views for overview data

### 3. Data to Display
- Limit the number of columns in views
- Avoid heavy calculated fields in list views
- Use simple field references when possible

### View Optimization Strategies

#### 1. Create Efficient Filters
```javascript
// Use indexed fields for better performance
CreatedDate >= date(2023, 1, 1) and Status = "Active"
```

#### 2. Optimize Calculated Fields
```javascript
// Cache calculated values in stored fields when possible
// Instead of calculating age every time, store and update it
Age := age(Birthdate)  // Update via trigger on Birthdate changes
```

#### 3. Use Appropriate Field Types
- Use choice fields instead of text fields for categories
- Use number fields for numeric data
- Use date fields for dates

---

## Performance Tips and Tricks

### General Performance Checklist

#### ✅ Data Structure
- Are tables properly related?
- Are indexes used effectively?
- Are field types appropriate?
- Is data normalized appropriately?

#### ✅ Queries and Filters
- Are filters using indexed fields?
- Are date ranges specific?
- Are complex calculations avoided in filters?
- Are views limited to necessary data?

#### ✅ Scripts and Formulas
- Are expensive calculations cached?
- Are loops optimized with transactions?
- Are server operations batched?
- Are unnecessary operations avoided?

#### ✅ User Interface
- Are views showing only necessary columns?
- Are large datasets paginated?
- Is user feedback provided for long operations?
- Are heavy operations moved to background?

### Specific Optimization Techniques

#### 1. Database Design
```javascript
// Use appropriate field types
Status := choice("Draft", "Active", "Archived")  // Not text field
CreatedDate := today()  // Use date field, not text
```

#### 2. Query Optimization
```javascript
// Good: Specific date range with indexed field
select Orders where CreatedDate >= date(2023, 1, 1) and CreatedDate <= today()

// Avoid: Open-ended queries
select Orders where contains(Description, "keyword")
```

#### 3. Calculation Optimization
```javascript
// Cache complex calculations
let complexResult := cached(
    sum((select OrderItems where OrderId = Id).Amount)
);
```

#### 4. Memory Management
```javascript
// Process large datasets in chunks
let allRecords := select LargeTable;
let chunkSize := 100;

for i from 0 to count(allRecords) step chunkSize do
    let chunk := slice(allRecords, i, i + chunkSize);
    do as transaction
        for record in chunk do
            // Process record
        end
    end
end
```

### Common Performance Pitfalls

#### ❌ Avoid These Patterns

1. **Unoptimized Loops**
```javascript
// Bad: No transaction context
for record in manyRecords do
    record.Field := value;
end
```

2. **Complex View Calculations**
```javascript
// Bad: Heavy calculation in list view
sum((select Related where ParentId = Id).Amount)
```

3. **Inefficient Filtering**
```javascript
// Bad: String operations in filters
contains(upper(Name), "SEARCH")
```

4. **Excessive Server Calls**
```javascript
// Bad: Multiple separate calls
let val1 := serverFunction1();
let val2 := serverFunction2();
let val3 := serverFunction3();
```

### Performance Monitoring

#### Key Metrics to Monitor
1. **Query execution time**
2. **Script execution time**
3. **View loading time**
4. **User interaction responsiveness**
5. **Memory usage**

#### Diagnostic Techniques
1. Use `sleep()` function to simulate delays for testing
2. Add timing logs to identify bottlenecks
3. Monitor database query performance
4. Test with production-sized datasets

---

## Advanced Performance Techniques

### Server-Side Processing
```javascript
// Move complex operations to server
function processDataOnServer() do
    do as server
        let data := select LargeTable where ComplexCondition;
        let processed := for item in data do
            // Complex processing
            processItem(item)
        end;
        processed
    end
end
```

### Asynchronous Operations
```javascript
// Use deferred execution for non-critical operations
do as deferred
    // Logging, notifications, etc.
    sendEmail(admin, "Process Complete", details);
    updateStatistics();
end
```

### Batch Processing
```javascript
// Process records in optimized batches
function batchUpdate(records, batchSize) do
    for i from 0 to count(records) step batchSize do
        do as transaction
            let batch := slice(records, i, i + batchSize);
            for record in batch do
                updateRecord(record);
            end
        end
    end
end
```

---

## Conclusion

Performance optimization in Ninox requires understanding:
1. **Transaction contexts** and their appropriate use
2. **Script execution** patterns and optimization
3. **Database query** efficiency
4. **User interface** responsiveness

By following these guidelines and continuously monitoring performance, you can build responsive and efficient Ninox applications that scale well with data growth.

---

**Source**: Ninox Community Documentation - Performance Section  
**Total Articles**: 7  
**Language**: German (translated content)
