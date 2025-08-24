# Find References

## Function Description (Replaces FindReferencingSymbolsTool)

When user requests to find all places where a specific symbol is used or referenced, execute the following workflow to locate references with context code and metadata:

## Step 1: Identify Target Symbol
**Description**: Specify the symbol to find references for
**Requirements**:
- Symbol must be defined in a specific file (not directory)
- Use same name path logic as symbol search
- Support hierarchical symbol paths (class/method)

**Symbol Identification Examples**:
```
# Method reference
Target: "login" method in "src/models/user.py"
→ Find where "login" method is called

# Class reference
Target: "User" class in "src/models/user.py"
→ Find where "User" class is instantiated or inherited

# Function reference
Target: "process_data" function in "src/utils/helpers.py"
→ Find where "process_data" function is called

# Variable reference
Target: "config" variable in "src/config.py"
→ Find where "config" variable is accessed
```

## Step 2: Configure Reference Search
**Description**: Set search parameters and filters for reference finding
**Search Configuration**:
- **Context level**: How much code context to show around references
- **Symbol filters**: Types of referencing symbols to include/exclude
- **Scope restrictions**: Limit search area

**Context Level Options**:
```
# Minimal context
→ Just the line with the reference

# Standard context (default)
→ 3-5 lines around the reference

# Extended context
→ 7-10 lines around the reference

# Full method context
→ Entire method/function containing the reference
```

**Filter Options**:
```
# Include specific symbol types
→ Filter: methods only, classes only, etc.

# Exclude certain areas
→ Filter: exclude tests, exclude imports

# Same file only
→ Filter: references in same file only
```

## Step 3: Execute Reference Search
**Description**: Perform search and collect reference information
**Search Process**:
- Find all locations where the symbol is referenced
- Collect metadata about referencing symbols
- Gather context code around each reference
- Format results with location information

**Reference Types**:
```
# Method calls
user.login(password)
result = user.login(credentials)

# Class instantiation
user = User(username, email)
admin = User.create_admin(data)

# Import references
from models.user import User
import models.user as user_module

# Type annotations
def process_user(user: User) -> bool:
    pass
```

## Step 4: Format Reference Results
**Description**: Structure reference information with context and metadata
**Output Structure**:
- **Referencing symbol**: Information about the symbol containing the reference
- **Reference location**: Exact line and column of the reference
- **Reference context**: Code snippet showing the reference usage

**Result Format**:
```json
{
  "referencing_symbol": {
    "name_path": "ContainingClass/method_name",
    "kind": 6,
    "relative_path": "path/to/file.py",
    "body_location": {
      "start_line": 10,
      "end_line": 20
    }
  },
  "reference_location": {
    "line": 15,
    "column": 25
  },
  "reference_context": "Code snippet showing the reference"
}
```

## Complete Workflow Examples

### Example 1: Find Method Usage
**Request**: "Find all references to login method in src/models/user.py, showing standard context"

#### Step 1: Identify target
```
Target symbol: "login" method
Source file: "src/models/user.py"
Context level: standard (3-5 lines)
```

#### Step 2: Execute search
```
Search for: references to "login"
In symbol: method from user.py
Include context: 2-3 lines before/after
```

#### Step 3: Expected output
```json
[
  {
    "referencing_symbol": {
      "name_path": "AuthController/authenticate",
      "kind": 6,
      "relative_path": "src/controllers/auth_controller.py",
      "body_location": {
        "start_line": 25,
        "end_line": 35
      }
    },
    "reference_location": {
      "line": 30,
      "column": 20
    },
    "reference_context": "def authenticate(self, username, password):\n    user = User.find_by_username(username)\n    if user and user.login(password):  # <- Reference here\n        return self.create_session(user)\n    return None"
  }
]
```

### Example 2: Find Class Usage
**Request**: "Find all references to Tool class in src/tools/tools_base.py, exclude imports"

#### Step 1: Identify target
```
Target symbol: "Tool" class
Source file: "src/tools/tools_base.py"
Filters: exclude imports (exclude_kinds=[2])
```

#### Step 2: Execute search
```
Search for: references to "Tool"
In symbol: class from tools_base.py
Exclude: import statements
```

### Example 3: Find Function References with Extended Context
**Request**: "Find all references to execute_shell_command in src/util/shell.py, showing extended context"

#### Step 1: Identify target
```
Target symbol: "execute_shell_command" function
Source file: "src/util/shell.py"
Context level: extended (7-10 lines)
```

#### Step 2: Execute search
```
Search for: references to "execute_shell_command"
In symbol: function from shell.py
Include context: extended (more lines)
```

## Reference Context Types

### 1. Method Calls
```python
# Direct method call
user.login(password)

# Chained method call
user.authenticate().login(credentials)

# Assignment with method call
result = user.login(password)
```

### 2. Class Instantiation
```python
# Direct instantiation
user = User(username, email)

# Factory pattern
user = UserFactory.create_user(data)

# Inheritance
class AdminUser(User):
    pass
```

### 3. Import References
```python
# Direct import
from models.user import User

# Module import
import models.user as user_module

# Aliased import
from models import User as UserModel
```

### 4. Type Annotations
```python
# Parameter annotation
def process_user(user: User) -> bool:
    pass

# Return type annotation
def get_user() -> User:
    pass

# Variable annotation
current_user: User = None
```

## Advanced Use Cases

### 1. Impact Analysis
**Request**: "Find all references to DatabaseConnection class"
- Understand what will be affected by changes
- Plan refactoring strategy

### 2. API Usage Discovery
**Request**: "Find all references to send_email function, exclude tests"
- See how API is being used
- Understand usage patterns

### 3. Dependency Mapping
**Request**: "Find all references to Config class"
- Map configuration dependencies
- Understand configuration flow

### 4. Dead Code Detection
**Request**: "Find all references to legacy_process function"
- Check if old code is still used
- Safe to remove if no references

## Filtering Options

### By Symbol Kind
- **Classes only**: `include_kinds=[5]`
- **Methods only**: `include_kinds=[6]`
- **Functions only**: `include_kinds=[12]`
- **Exclude imports**: `exclude_kinds=[2]`

### By Location
- **Same package**: References within same directory tree
- **Cross-package**: References from other packages
- **Test exclusion**: Skip test directories

## Common Patterns

### Before Refactoring
1. Find the symbol definition
2. Find all references
3. Analyze usage patterns
4. Plan safe refactoring approach

### Debugging
1. Find where error-causing method is called
2. Check context of each call
3. Identify problematic usage

### Code Review
1. Find references to new/modified symbols
2. Verify proper usage
3. Check for potential issues

## Error Handling

### No References Found
- Verify the symbol exists in the specified file
- Check for typos in symbol name
- Ensure file path is correct
- Symbol might be unused (dead code)

### Too Many Results
- Add filters to focus on relevant references
- Exclude test files if not needed
- Use more specific symbol paths
- Limit to specific symbol kinds

### Missing Expected References
- Check for aliased imports
- Look for dynamic references (getattr, etc.)
- Verify scope of search
- Consider indirect references through inheritance

## Tips for Better Results

### 1. Start with the Definition File
Always provide the exact file where the symbol is defined:
```
✅ "Find references to login in src/models/user.py"
❌ "Find references to login in models/"
```

### 2. Use Specific Symbol Paths
For methods within classes, be specific:
```
✅ "Find references to User/save in src/models/user.py"
❌ "Find references to save"
```

### 3. Consider Context Needs
- **Debugging**: Use extended context
- **Quick overview**: Use minimal context
- **Code review**: Use standard context

### 4. Filter Appropriately
- **Production analysis**: Exclude tests
- **Complete analysis**: Include everything
- **Refactoring**: Focus on specific symbol types

This workflow replaces FindReferencingSymbolsTool functionality for locating symbol usage across codebases.