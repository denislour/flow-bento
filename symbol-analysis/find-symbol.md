# Find Symbol

## Function Description (Replaces FindSymbolTool)

When user requests to find symbols/code entities (classes, methods, functions, variables) based on name patterns with filtering options, execute the following workflow using natural language:

## Step 1: Define Search Parameters
**Description**: Specify what type of symbol to search for and search scope
**Search Requirements**:
- Define symbol type (class, method, function, variable, constructor)
- Set search pattern (exact name, substring, name path)
- Determine search scope (entire project, specific directory, or file)

**Symbol Type Examples**:
```
# Classes
User: "Find class UserService"
→ Search: "UserService", filter class type (kind=5)

# Methods
User: "Find method authenticate in UserService"
→ Search: "UserService/authenticate", filter method type (kind=6)

# Functions
User: "Find function processData"
→ Search: "processData", filter function type (kind=12)

# Variables
User: "Find variable config"
→ Search: "config", filter variable type (kind=13)
```

## Step 2: Execute Search with Filters
**Description**: Perform code search with appropriate filters and scope
**Search Options**:
- **Exact matching**: Find symbols with exact name
- **Substring matching**: Find symbols containing the pattern
- **Path matching**: Find symbols using hierarchical paths (class/method)
- **Scope restriction**: Limit search to specific files or directories

**Name Path Matching Behavior**:
- Simple name (e.g., "method"): Matches any symbol named "method" anywhere
- Relative path (e.g., "class/method"): Matches method within any class
- Absolute path (e.g., "/class/method"): Matches method only in top-level class

**Language-Specific Examples**:
```
# Python
Search: "def login" within "src/models/" directory
→ Find method definitions containing "login"

# Ruby
Search: "class User" within "app/models/" directory
→ Find class definitions named "User"

# Java
Search: "processPayment" within "src/main/java/" directory
→ Find methods named "processPayment"

# JavaScript
Search: "function handleRequest" in entire project
→ Find function definitions containing "handleRequest"
```

## Step 3: Filter Results by Symbol Kind
**Description**: Apply symbol kind filters to get relevant results
**Symbol Kinds**:
- **1** = file
- **2** = module
- **5** = class
- **6** = method
- **9** = constructor
- **12** = function
- **13** = variable
- **14** = constant

**Filter Examples**:
```
# Classes only
→ Apply filter: include_kinds=[5]

# Methods only
→ Apply filter: include_kinds=[6]

# Functions only
→ Apply filter: include_kinds=[12]

# Classes and methods
→ Apply filter: include_kinds=[5,6]

# Exclude imports/modules
→ Apply filter: exclude_kinds=[2]
```

## Step 4: Retrieve Symbol Details & Create Context Memory
**Description**: Get symbol information and automatically store insights for future reference
**Detail Levels**:
- **Metadata only**: Symbol names, types, and locations
- **With children**: Include nested symbols (methods in classes)
- **With source code**: Include actual code content
- **Full details**: Everything above combined

**Memory Creation Protocol**:
- Store discovered symbol locations in project memory
- Record architectural patterns found during search
- Save common symbol naming conventions
- Document frequently accessed code areas

**Detail Examples**:
```
# Basic symbol info
→ Return: name_path, kind, relative_path, body_location
→ Memory: Store symbol location for quick future access

# With children (depth=1)
→ Return: class with all its methods
→ Memory: Store class architecture and method organization

# With source code
→ Return: symbol with actual implementation code
→ Memory: Store code patterns and implementation insights

# Full details
→ Return: complete symbol information including children and code
→ Memory: Store comprehensive symbol knowledge for project understanding
```

**Automatic Memory Creation**:
```
# After successful symbol discovery:
1. Create memory with symbol locations found
2. Store architectural insights discovered
3. Record user search patterns for optimization
4. Update project symbol map for faster future searches
```

## Complete Workflow Examples

### Example 1: Find Specific Class
**Request**: "Find class Tool in entire project, with children and metadata only"

#### Step 1: Define search
```
Target: class named "Tool"
Scope: entire project
Details: metadata + children
```

#### Step 2: Execute search
```
Search pattern: "Tool"
Symbol filter: classes only (kind=5)
Include children: depth=1
Source code: exclude
```

#### Step 3: Expected output
```json
[
  {
    "name_path": "Tool",
    "kind": 5,
    "relative_path": "src/tools/tools_base.py",
    "body_location": {
      "start_line": 95,
      "end_line": 180
    },
    "children": [
      {
        "name_path": "Tool/get_name",
        "kind": 6,
        "body_location": {"start_line": 110, "end_line": 112}
      },
      {
        "name_path": "Tool/apply",
        "kind": 6,
        "body_location": {"start_line": 120, "end_line": 125}
      }
    ]
  }
]
```

### Example 2: Find Methods by Pattern
**Request**: "Find methods starting with 'get_' in tools directory, metadata only"

#### Step 1: Define search
```
Target: methods with names starting with "get_"
Scope: tools directory
Details: metadata only
```

#### Step 2: Execute search
```
Search pattern: "get_" with substring matching
Symbol filter: methods only (kind=6)
Scope: "src/tools/" directory
Source code: exclude
```

### Example 3: Find Constructor with Source Code
**Request**: "Find constructor in ReadFileTool class, with source code"

#### Step 1: Define search
```
Target: constructor in specific class
Scope: ReadFileTool class
Details: with source code
```

#### Step 2: Execute search
```
Search pattern: "ReadFileTool/__init__"
Symbol filter: constructor (kind=9)
Source code: include
```

## Advanced Search Patterns

### Name Path Matching
- `"method"` - Matches any method named "method" anywhere
- `"Class/method"` - Method "method" within any "Class"
- `"/TopClass/method"` - Method only in top-level "TopClass"

### Search Scope Options
- **Entire project**: Search all files
- **Specific directory**: Limit to directory tree
- **Single file**: Search within one file only

### Filtering Strategies
- **By symbol type**: Include/exclude specific kinds
- **By location**: Same package vs cross-package references
- **By visibility**: Public vs private symbols

## Common Use Cases

### 1. Understanding New Codebase
**Request**: "Find all classes in entire project, with children"
- Discover main classes and their methods
- Understand code structure

### 2. Finding Implementation
**Request**: "Find function named process_data in src/ directory, with source code"
- Locate specific function implementation
- See actual code content

### 3. API Discovery
**Request**: "Find all methods starting with 'handle_' in controllers directory"
- Discover API endpoints
- Understanding request handling

### 4. Refactoring Preparation
**Request**: "Find class User in entire project, with full details"
- Get complete class information before refactoring
- Understand class structure and dependencies

## Error Handling

### No Results Found
- Check spelling of symbol name
- Verify scope includes the target location
- Try substring matching for partial names
- Broaden the search scope

### Too Many Results
- Add more specific filters (include_kinds)
- Narrow the scope to specific directories
- Use more specific name patterns
- Exclude irrelevant areas (tests, generated code)

## Tips for Better Results

1. **Start broad, then narrow**: Begin with general searches, then add filters
2. **Use appropriate scope**: Limit to specific directories when possible
3. **Specify symbol types**: Use symbol kind filters to focus on relevant symbols
4. **Consider name paths**: Use hierarchical patterns for nested symbols
5. **Include children for classes**: Use depth > 0 to see class methods

This workflow replaces FindSymbolTool functionality for discovering code symbols across different programming languages.