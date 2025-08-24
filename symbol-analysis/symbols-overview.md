# Symbols Overview

## Function Description (Replaces GetSymbolsOverviewTool)

When user requests to get an overview of top-level symbols defined in a file, execute the following workflow to understand code structure and organization:

## Step 1: Specify Target File
**Description**: Identify the file to analyze for symbol overview
**Requirements**:
- Must be a specific file, not a directory
- File must exist within the project
- Relative path from project root

**File Specification Examples**:
```
# Python files
Target: "src/models/user.py"
→ Get overview of classes and functions in user.py

# Ruby files
Target: "app/models/order.rb"
→ Get overview of classes and methods in order.rb

# Java files
Target: "src/main/java/com/example/UserService.java"
→ Get overview of classes and methods in UserService.java

# JavaScript files
Target: "src/services/api.js"
→ Get overview of functions and classes in api.js
```

## Step 2: Extract Top-Level Symbols
**Description**: Identify and catalog top-level symbols in the file
**Symbol Categories**:
- **Classes**: Class definitions with their basic structure
- **Functions**: Top-level function definitions
- **Variables**: Module-level variables and constants
- **Imports**: Import statements and dependencies

**Symbol Information Collected**:
```
# Basic symbol data
- Symbol name and type
- Location (start/end lines)
- Symbol kind (class=5, method=6, function=12, etc.)
- Relative path information

# Structural information
- Symbol hierarchy
- Basic relationships
- Accessibility (public/private)
```

## Step 3: Organize Symbol Hierarchy
**Description**: Structure symbols to show file organization
**Organization Principles**:
- Top-level symbols first
- Nested symbols under their parents
- Maintain source code order
- Show symbol relationships

**Hierarchy Examples**:
```
# Python file structure
File: user.py
├── Import statements
├── Constants/Variables
├── Class User
│   ├── __init__ method
│   ├── login method
│   └── logout method
└── Helper functions

# Java file structure
File: UserService.java
├── Package declaration
├── Import statements
├── Class UserService
│   ├── Constructor
│   ├── Public methods
│   └── Private methods
└── Static utility methods
```

## Step 4: Format Overview Output
**Description**: Present symbol information in structured format
**Output Format**:
- JSON structure with symbol metadata
- Hierarchical organization
- Location information for each symbol
- Symbol type identification

**Standard Output Structure**:
```json
[
  {
    "name": "User",
    "kind": 5,
    "location": {
      "start_line": 10,
      "end_line": 45
    },
    "children": [
      {
        "name": "__init__",
        "kind": 9,
        "location": {
          "start_line": 11,
          "end_line": 15
        }
      },
      {
        "name": "login",
        "kind": 6,
        "location": {
          "start_line": 17,
          "end_line": 25
        }
      }
    ]
  }
]
```

## Complete Workflow Examples

### Example 1: Python File Overview
**Request**: "Get symbols overview for src/models/user.py"

#### Step 1: Specify file
```
Target file: "src/models/user.py"
File type: Python module
Analysis scope: top-level symbols
```

#### Step 2: Extract symbols
```
Discovered symbols:
- Class: User (lines 10-45)
- Function: validate_email (lines 47-52)
- Variable: DEFAULT_ROLE (line 5)
```

#### Step 3: Expected output
```json
[
  {
    "name": "DEFAULT_ROLE",
    "kind": 13,
    "location": {
      "start_line": 5,
      "end_line": 5
    }
  },
  {
    "name": "User",
    "kind": 5,
    "location": {
      "start_line": 10,
      "end_line": 45
    }
  },
  {
    "name": "validate_email",
    "kind": 12,
    "location": {
      "start_line": 47,
      "end_line": 52
    }
  }
]
```

### Example 2: Java File Overview
**Request**: "Get symbols overview for src/main/java/com/example/UserService.java"

#### Step 1: Specify file
```
Target file: "src/main/java/com/example/UserService.java"
File type: Java class
Analysis scope: class members
```

#### Step 2: Extract symbols
```
Discovered symbols:
- Class: UserService (lines 15-120)
  - Constructor: UserService (lines 20-25)
  - Method: createUser (lines 27-35)
  - Method: findUser (lines 37-42)
  - Method: deleteUser (lines 44-50)
```

### Example 3: Ruby File Overview
**Request**: "Get symbols overview for app/models/order.rb"

#### Step 1: Specify file
```
Target file: "app/models/order.rb"
File type: Ruby class
Analysis scope: class and module definitions
```

#### Step 2: Extract symbols
```
Discovered symbols:
- Class: Order (lines 5-85)
  - Method: initialize (lines 10-15)
  - Method: calculate_total (lines 17-25)
  - Method: add_item (lines 27-35)
  - Private methods section (lines 40-80)
```

## Use Cases

### 1. Understanding New Files
**Scenario**: First time exploring a codebase
**Process**:
1. Get symbols overview of main files
2. Understand file structure and organization
3. Identify key classes and functions
4. Plan deeper investigation

### 2. Code Review Preparation
**Scenario**: Reviewing changes in specific files
**Process**:
1. Get overview of modified files
2. Understand current structure
3. Compare with changes
4. Assess impact of modifications

### 3. Refactoring Planning
**Scenario**: Planning to refactor large files
**Process**:
1. Get complete symbols overview
2. Identify refactoring candidates
3. Understand symbol dependencies
4. Plan safe refactoring approach

### 4. API Documentation
**Scenario**: Generating documentation
**Process**:
1. Get overview of public interfaces
2. Identify exported functions/classes
3. Document public APIs
4. Generate interface specifications

## Symbol Kind Reference

### Common Symbol Kinds
- **1** = file
- **2** = module
- **5** = class
- **6** = method
- **9** = constructor
- **12** = function
- **13** = variable
- **14** = constant

### Language-Specific Considerations

#### Python
- Module-level functions (kind=12)
- Class definitions (kind=5)
- Class methods (kind=6)
- Module variables (kind=13)

#### Java
- Class definitions (kind=5)
- Constructor methods (kind=9)
- Instance methods (kind=6)
- Static methods (kind=6)

#### Ruby
- Class definitions (kind=5)
- Instance methods (kind=6)
- Class methods (kind=6)
- Module definitions (kind=2)

#### JavaScript/TypeScript
- Function declarations (kind=12)
- Class definitions (kind=5)
- Method definitions (kind=6)
- Variable declarations (kind=13)

## Best Practices

### 1. Start with Overview
Always get symbols overview before detailed analysis:
```
✅ Overview first → Targeted reading
❌ Random file reading → Confusion
```

### 2. Use for Navigation
Overview provides navigation roadmap:
```
✅ Overview → Find interesting symbols → Read details
❌ Search blindly → Miss important code
```

### 3. Understand Structure
Use overview to understand file organization:
```
✅ See overall structure → Understand design
❌ Focus on details only → Miss big picture
```

### 4. Plan Further Actions
Use overview to plan next steps:
```
✅ Overview → Plan investigation → Execute
❌ Dive deep immediately → Get lost
```

## Error Handling

### File Not Found
- Verify file path is correct
- Check file exists in project
- Ensure proper relative path format

### Empty Overview
- File might have no top-level symbols
- File might be empty or only comments
- Check if file contains only imports

### Large Files
- Overview might be truncated for very large files
- Focus on specific sections if needed
- Consider file splitting if too complex

## Integration with Other Operations

### Before Symbol Search
1. Get symbols overview
2. Identify interesting symbols
3. Use targeted symbol search

### Before File Reading
1. Get symbols overview
2. Understand file structure
3. Read specific sections

### Before Modifications
1. Get symbols overview
2. Understand current structure
3. Plan safe modifications

This workflow replaces GetSymbolsOverviewTool functionality for understanding file structure and symbol organization.