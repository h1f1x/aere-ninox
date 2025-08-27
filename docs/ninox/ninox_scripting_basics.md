# Ninox Scripting Basics - Complete Guide

## Table of Contents
1. [Introduction to Ninox Script](#introduction)
2. [Formula Editor](#formula-editor)
3. [Operators](#operators)
4. [Variables](#variables)
5. [Control Structures](#control-structures)
6. [Data Operations](#data-operations)
7. [Loops](#loops)
8. [Custom Functions](#custom-functions)
9. [Transactions](#transactions)
10. [Triggers](#triggers)

## Introduction

The Ninox scripting language (also called "NX scripting language" or "NX script") is designed for simple, recurring automation tasks that improve workflows. These scripts are executed via the formula editor within various field types.

## Formula Editor

The input of functions or procedures takes place via the formula editor in a formula field (always marked with fx). These fields are the "gateway" to the formula editor.

### Formula Editor Features (Version 3.6+)
- Syntax highlighting
- Auto-completion
- Error detection
- Code formatting
- Search and replace functionality

## Operators

### Arithmetic Operators
Used for simple calculations with numeric values:

```javascript
+   // Addition: 5 + 3 = 8
-   // Subtraction: 10 - 4 = 6  
*   // Multiplication: 6 * 7 = 42
/   // Division: 15 / 3 = 5
%   // Modulo: 17 % 5 = 2
```

### Comparison Operators
Compare two values and return true or false:

```javascript
=   // Equal to: 5 = 5 returns true
!=  // Not equal to: 5 != 3 returns true
<   // Less than: 3 < 5 returns true
<=  // Less than or equal to: 3 <= 3 returns true
>   // Greater than: 7 > 4 returns true
>=  // Greater than or equal to: 5 >= 5 returns true
```

### Ninox Operators
Special operators for Ninox scripting:

```javascript
:=  // Assignment: assigns a value to a field or variable
.   // Field access: accesses fields of related records
[]  // Array access: accesses array elements
and // Logical AND
or  // Logical OR
not // Logical NOT
```

## Variables

### Declaring Variables
Use `let` to create new variables:

```javascript
let myVariable := "Hello World";
let numberVar := 42;
let dateVar := today();
```

**Important**: Variable names cannot be keywords (e.g., `let let` is forbidden).

## Control Structures

### Simple Branching (if-then-else)
```javascript
if condition then
    // code if true
else
    // code if false
end
```

### Multiple Branching
```javascript
if condition1 then
    // code for condition1
else if condition2 then
    // code for condition2
else if condition3 then
    // code for condition3
else
    // default code
end
```

### Switch Statement
```javascript
switch value do
case "option1":
    // code for option1
case "option2":
    // code for option2
default:
    // default code
end
```

## Data Operations

### Selecting Records
```javascript
select TableName where condition
```

Example:
```javascript
select Customers where Age > 18
```

### Creating Records
```javascript
create TableName
```

### Deleting Records
```javascript
delete record
```

### Sorting Records
```javascript
order by FieldName
order by FieldName desc  // descending
```

## Loops

### For Loop (with array)
```javascript
for item in array do
    // process each item
end
```

### For Loop (numeric range)
```javascript
for i from 1 to 10 do
    // repeat 10 times
end
```

### While Loop
```javascript
while condition do
    // repeat while condition is true
end
```

## Custom Functions

Create reusable functions:

```javascript
function myFunction(parameter1, parameter2) do
    // function body
    parameter1 + parameter2  // return value
end
```

Call the function:
```javascript
myFunction(5, 3)  // returns 8
```

## Transactions

### Reading Transactions
Used when filtering or searching for specific records in a table.

### Writing Transactions
Used when data is changed, including:
- Data entry or modification
- Individual calculations
- Script execution

### Transaction Control
```javascript
do as transaction
    // transactional operations
end

do as server
    // server-side operations
end

do as deferred
    // deferred operations
end
```

## Triggers

Triggers are automated scripts that execute when certain conditions are met.

### Field-Level Triggers
Triggers can be attached to individual fields and execute when:
- Field value changes
- Record is created
- Record is modified
- Record is deleted

### Button Triggers
Execute scripts when buttons are clicked:

```javascript
// Button script example
alert("Button clicked!");
Name := "New Value";
```

## Dynamic Text Creation

Create personalized text using variables and field values:

```javascript
"Hello " + CustomerName + ", your order #" + OrderNumber + " is ready."
```

## Automatic Adjustments

Ninox automatically optimizes your scripts by:
- Removing unnecessary parentheses in expressions
- Optimizing calculations
- Converting data types when needed

## Date and Time Formats

Ninox supports various date and time format tokens:
- `YYYY` - 4-digit year
- `MM` - 2-digit month  
- `DD` - 2-digit day
- `HH` - 24-hour format hour
- `mm` - minutes
- `ss` - seconds

## Supported Languages

Ninox supports multiple languages for date/time formatting and localization. The system automatically detects the user's browser/app language setting.

## Best Practices

1. **Use descriptive variable names**
2. **Comment complex logic**
3. **Break down complex operations into smaller functions**
4. **Use transactions appropriately for data consistency**
5. **Test scripts with different data scenarios**
6. **Optimize for performance with large datasets**

---

**Note**: This guide covers the fundamental concepts. For detailed function references, see the Functions Reference document.

**Source**: Ninox Community Documentation
**Language**: German (translated content)
