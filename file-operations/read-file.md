# Read File

## Function Description (Replaces ReadFileTool)

When user requests to read file contents within the project directory, execute the following workflow to access file content with options for partial reading, line ranges, and content length limiting:

## Step 1: Specify File and Range
**Description**: Define the file to read and specify reading parameters
**Requirements**:
- File must be within project directory
- Use relative path from project root
- Specify reading range (optional)
- Set content length limits (optional)

**File Specification Examples**:
```
# Complete file reading
Target: "src/main.py"
→ Read entire file content

# Line range reading
Target: "src/models/user.py" lines 10-50
→ Read specific line range (0-based indexing)

# Limited content reading
Target: "docs/README.md" max 5000 characters
→ Read file with character limit
```

## Step 2: Validate File Access
**Description**: Ensure file exists and is accessible within project
**Validation Requirements**:
- File must exist in project directory
- File must not be in gitignored paths
- File path must be relative to project root
- File must be readable (not binary unless specified)

**Path Validation Examples**:
```
# Valid relative paths
✅ "src/main.py"           → /project/src/main.py
✅ "docs/README.md"        → /project/docs/README.md
✅ ".github/workflows/ci.yml" → /project/.github/workflows/ci.yml

# Invalid paths
❌ "/absolute/path/file.py"    → Error: must be relative
❌ "../outside/project.py"     → Error: outside project
❌ "node_modules/package.json" → Error: gitignored
```

## Step 3: Read File Content
**Description**: Extract file content according to specified parameters
**Reading Options**:
- **Entire file**: Read complete file content
- **Line range**: Read specific lines (start_line to end_line)
- **Character limit**: Truncate content if exceeds limit
- **Encoding**: Handle UTF-8 encoding properly

**Reading Modes**:
```
# Complete file reading
→ Read from start to end of file

# Line range reading (0-based indexing)
→ Read lines 25-75 (51 lines total)
→ Read lines 0-49 (first 50 lines)
→ Read lines 100- (from line 101 to end)

# Character-limited reading
→ Read up to 5000 characters
→ Truncate if content exceeds limit
```

## Step 4: Format and Return Content
**Description**: Process and format the file content for output
**Output Formatting**:
- Preserve original formatting and indentation
- Include line break characters
- Provide content metadata (file path, line numbers)
- Handle truncation indicators

**Output Examples**:
```
# Complete file output
Contents of src/example.py:
```python
def example_function():
    """Example function docstring."""
    return "Hello, World!"
```

# Partial content with range info
Contents of src/example.py, lines 10-20:
```python
    def process_data(self, data):
        """Process the input data."""
        if not data:
            return None
        return processed_data
```

# Truncated content warning
Contents of src/large_file.py (truncated at 5000 characters):
```python
# Large file content...
# ... [Content truncated due to length limit] ...
```
```

## Complete Workflow Examples

### Example 1: Read Entire File
**Request**: "Read file src/models/user.py with entire file"

#### Step 1: Specify parameters
```
File: "src/models/user.py"
Range: entire file
Limit: unlimited
```

#### Step 2: Validate access
```
Check: file exists in project
Check: not in gitignore
Check: readable format
```

#### Step 3: Read content
```
Read: complete file from start to end
Format: preserve original structure
```

#### Step 4: Expected output
```python
import bcrypt
from datetime import datetime

class User:
    def __init__(self, username, email):
        self.username = username
        self.email = email
        self.created_at = datetime.now()
    
    def login(self, password):
        return bcrypt.check(password, self.password_hash)
```

### Example 2: Read Specific Line Range
**Request**: "Read file src/services/auth.py with lines 50-100"

#### Step 1: Specify parameters
```
File: "src/services/auth.py"
Range: lines 50-100 (0-based indexing)
Limit: unlimited
```

#### Step 2: Read content
```
Read: lines 50 through 100 (inclusive)
Total: 51 lines
```

#### Step 3: Expected output
```python
Contents of src/services/auth.py, lines 50-100:

    def authenticate_user(self, credentials):
        """Authenticate user with provided credentials."""
        username = credentials.get('username')
        password = credentials.get('password')
        
        if not username or not password:
            return None
            
        user = self.user_repository.find_by_username(username)
        if user and user.verify_password(password):
            return self.create_session(user)
        return None
```

### Example 3: Read with Character Limit
**Request**: "Read file README.md with max 2000 chars"

#### Step 1: Specify parameters
```
File: "README.md"
Range: entire file
Limit: 2000 characters maximum
```

#### Step 2: Read and truncate
```
Read: complete file
Check: content length > 2000 chars
Action: truncate and add warning
```

## Line Range Specifications

### Zero-Based Indexing
- **Line 0** = First line of the file
- **Line 10** = Eleventh line of the file
- **Lines 0-9** = First 10 lines

### Range Examples
```
"lines 0-49"     → First 50 lines
"lines 100-199"  → Lines 101-200 (human counting)
"lines 50-"      → From line 51 to end
"lines -10"      → Last 10 lines (if supported)
```

### Practical Line Ranges
```
# Class definition
"lines 45-120"   → Full class implementation

# Method body
"lines 67-85"    → Specific method

# File header
"lines 0-20"     → Imports and header comments

# Main function
"lines -50"      → Bottom of file where main() usually is
```

## File Type Handling

### Source Code Files
```python
# Python files (.py)
"src/models/user.py"

# JavaScript files (.js, .ts)
"frontend/src/components/App.tsx"

# Configuration files
"tsconfig.json"
```

### Documentation Files
```markdown
# Markdown files (.md)
"docs/api-documentation.md"

# Text files (.txt)
"requirements.txt"
```

### Configuration and Data Files
```yaml
# YAML files (.yml, .yaml)
"docker-compose.yml"

# JSON files (.json)
"package.json"

# Environment files (.env)
".env.example"
```

## Common Use Cases

### 1. Understanding Code Structure
**Request**: "Read file src/tools/base.py with lines 0-50"
- See imports and class definitions
- Understand file organization
- Identify main components

### 2. Examining Specific Function
**Request**: "Read file src/agent.py with lines 150-200"
- Focus on specific method implementation
- Understand algorithm details
- Debug specific functionality

### 3. Configuration Review
**Request**: "Read file pyproject.toml with entire file"
- Check project dependencies
- Understand build configuration
- Review project metadata

### 4. Documentation Reading
**Request**: "Read file CONTRIBUTING.md with max 3000 chars"
- Get overview of contribution instructions
- Understand project workflow
- Quick documentation review

## Integration with Symbol Analysis

### Before Symbol Search
1. **Read overview**: Read file with lines 0-30
2. **Identify symbols**: Use symbols overview
3. **Read specific symbols**: Use targeted reading

### After Finding Symbols
1. **Find symbol location**: Use symbol search to get line numbers
2. **Read implementation**: Read file with specific line range
3. **Understand context**: Read surrounding code

## Best Practices

### 1. Start with Overview
```
✅ Read file header first (lines 0-50)
✅ Then dive into specific sections
❌ Read entire large file immediately
```

### 2. Use Appropriate Ranges
```
✅ "Read lines 25-75" for function-sized chunk
✅ "Read entire file" for small config files
❌ "Read entire file" for very large files
```

### 3. Combine with Symbol Analysis
```
Workflow:
1. Get symbols overview for file
2. Find symbol locations
3. Read specific line ranges for symbols
```

### 4. Respect File Types
```
✅ "Read entire file" for README.md (documentation)
✅ "Read lines 0-30" for code overview
✅ "Read entire file" for package.json (small config)
```

## Error Handling

### File Not Found
```
Error: "File not found: nonexistent.py"
Solution: Check file path spelling and existence
```

### Invalid Line Range
```
Error: "Line range exceeds file length"
Solution: Check file size first or use smaller range
```

### Access Denied
```
Error: "Access denied or file outside project"
Solution: Ensure file is within project and not gitignored
```

### File Too Large
```
Warning: "File truncated due to size"
Solution: Use line ranges or increase character limit
```

## Advanced Usage

### Reading for Different Purposes

#### Code Review
- Read specific line ranges around changes
- Focus on modified functions/classes
- Check imports and dependencies

#### Debugging
- Read error-prone sections
- Check configuration files
- Examine test files

#### Documentation
- Read README files
- Check API documentation
- Review setup instructions

#### Refactoring Planning
- Read existing implementation
- Understand current structure
- Identify dependencies

This workflow replaces ReadFileTool functionality for efficient file content access and reading operations.