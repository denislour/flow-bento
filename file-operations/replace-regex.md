# Replace Regex

## Function Description (Replaces ReplaceRegexTool)

When user requests to replace content in files using regular expressions, execute the following workflow to perform precise pattern-based text replacement:

## Step 1: Define Target File and Regex Pattern
**Description**: Specify the file to modify and the regex pattern to match content for replacement
**Pattern Definition Requirements**:
- Target file must exist and be within project boundaries
- Regular expression pattern to match content for replacement
- Replacement string (may include backreferences)
- Occurrence handling settings (single vs multiple matches)

**Regex Pattern Guidelines**:
```
# Use wildcards appropriately for flexibility
Pattern: "function.*?{" → Match function declarations
Pattern: "class.*?extends.*?{" → Match class inheritance
Pattern: "import.*?from.*?;" → Match import statements

# Avoid overly specific patterns
✅ Good: "constructor.*?{" (flexible function matching)
❌ Bad: "constructor(param1, param2, param3) {" (too specific)

# Use non-greedy quantifiers for precise matching
✅ Good: "start.*?end" (stops at first "end")
❌ Bad: "start.*end" (greedy, may match too much)
```

## Step 2: Configure Replacement Parameters
**Description**: Set up replacement string and occurrence handling options
**Replacement Configuration**:
- Define replacement text (may include regex backreferences)
- Specify whether to allow multiple occurrences in file
- Configure multiline and dotall regex flags
- Plan escape sequences for special characters

**Replacement String Features**:
```
# Backreferences for captured groups
Pattern: "(function\s+)(\w+)(\s*\(.*?\)\s*{)"
Replacement: "\1new\2\3" → Adds "new" prefix to function name

# Literal text replacement
Pattern: "oldFunctionName"
Replacement: "newFunctionName" → Simple text substitution

# Special character escaping
Replacement: "\\n" → Literal newline character
Replacement: "\\t" → Literal tab character
Replacement: "\\\\" → Literal backslash
```

## Step 3: Execute Regex Replacement
**Description**: Perform the pattern matching and replacement operation
**Replacement Execution**:
- Apply regex pattern with DOTALL and MULTILINE flags
- Perform substitution with specified replacement string
- Count number of matches and replacements made
- Validate occurrence constraints (single vs multiple)

**Regex Flags Applied**:
```
# DOTALL flag
→ Dot (.) matches all characters including newlines
→ Enables multiline pattern matching
→ Useful for matching code blocks across lines

# MULTILINE flag  
→ ^ and $ match start/end of lines, not just string
→ Enables line-by-line pattern matching
→ Useful for matching line-specific patterns
```

## Step 4: Validate and Return Results
**Description**: Confirm replacement success and handle any issues
**Result Validation**:
- Verify expected number of matches found
- Check replacement was successful
- Handle multiple occurrence scenarios appropriately
- Return success message or error information

**Validation Scenarios**:
```
# Successful single replacement
→ Pattern matched exactly once
→ Replacement applied successfully
→ File updated with new content

# Multiple occurrences handling
→ If allow_multiple_occurrences=true: Replace all matches
→ If allow_multiple_occurrences=false: Return error for multiple matches
→ Provide match count information

# No matches found
→ Pattern didn't match anything in file
→ Return error with pattern and file information
→ Suggest pattern refinement
```

## Complete Workflow Examples

### Example 1: Replace Function Name
**Request**: "Replace function 'oldProcess' with 'newProcess' in user_service.py"

#### Step 1: Define pattern
```
Target file: "src/services/user_service.py"
Pattern: "def oldProcess"
Replacement: "def newProcess"
Multiple occurrences: false (expect single function)
```

#### Step 2: Configure replacement
```
Regex pattern: "def oldProcess"
Replacement text: "def newProcess"
Backreferences: None needed
Special characters: None
```

#### Step 3: Execute replacement
```
Pattern matching: ✅ Found 1 occurrence
Replacement: "def oldProcess" → "def newProcess"
File update: ✅ Successful
```

#### Step 4: Expected result
```
Success: "Replaced 1 occurrence of pattern 'def oldProcess' in file 'src/services/user_service.py'"
```

### Example 2: Replace Import Statements with Wildcards
**Request**: "Update import statements to use new library path"

#### Step 1: Define flexible pattern
```
Target file: "src/components/App.js"
Pattern: "import.*?from ['\"]old-library['\"]"
Replacement: "import$1from 'new-library'"
Multiple occurrences: true (multiple imports expected)
```

#### Step 2: Configure with wildcards
```
Regex pattern: "import(.*?)from ['\"]old-library['\"]"
Replacement: "import\1from 'new-library'"
Backreference: \1 captures the import content
Flexibility: Handles various import formats
```

#### Step 3: Execute multiple replacements
```
Pattern matches: ✅ Found 3 occurrences
Replacements:
- "import { Component } from 'old-library'" → "import { Component } from 'new-library'"
- "import utils from 'old-library'" → "import utils from 'new-library'"  
- "import * as lib from 'old-library'" → "import * as lib from 'new-library'"
```

#### Step 4: Expected result
```
Success: "Replaced 3 occurrences of pattern in file 'src/components/App.js'"
```

### Example 3: Replace Method Implementation with Code Block
**Request**: "Replace getUserById method implementation with new logic"

#### Step 1: Define code block pattern
```
Target file: "src/models/User.java"
Pattern: "public User getUserById\\(.*?\\)\\s*\\{.*?\\}"
Replacement: "public User getUserById(Long id) {\n    return userRepository.findById(id).orElse(null);\n}"
Multiple occurrences: false (specific method)
```

#### Step 2: Configure multiline replacement
```
Regex pattern: "public User getUserById\\(.*?\\)\\s*\\{.*?\\}"
Replacement: "public User getUserById(Long id) {\n    return userRepository.findById(id).orElse(null);\n}"
Flags: DOTALL (for multiline matching)
Escaping: Parentheses and braces escaped in pattern
```

#### Step 3: Execute code block replacement
```
Pattern matching: ✅ Found 1 method implementation
Original code: Full method body replaced
New implementation: Updated with new logic
File update: ✅ Method successfully replaced
```

#### Step 4: Expected result
```
Success: "Replaced method implementation in file 'src/models/User.java'"
```

## Regex Pattern Best Practices

### Use Appropriate Wildcards
```
# Flexible patterns (recommended)
✅ "function.*?{" → Matches any function declaration
✅ "class.*?extends.*?{" → Matches class inheritance patterns
✅ "import.*?from.*?['\"].*?['\"]" → Matches various import formats

# Overly specific patterns (avoid)
❌ "function processUser(data) {" → Too rigid, breaks on formatting changes
❌ "class User extends BaseModel {" → Doesn't handle parameter variations
❌ "import { Component } from 'react'" → Misses other import styles
```

### Handle Multiline Content
```
# Code block patterns
Pattern: "try\\s*\\{.*?\\}\\s*catch.*?\\{.*?\\}"
→ Matches try-catch blocks across multiple lines

Pattern: "if\\s*\\(.*?\\)\\s*\\{.*?\\}"
→ Matches if statements with code blocks

Pattern: "/\\*.*?\\*/"
→ Matches multiline comments
```

### Use Backreferences Effectively
```
# Capture and preserve parts
Pattern: "(function\\s+)(\\w+)(\\s*\\(.*?\\))"
Replacement: "\\1async \\2\\3"
→ Adds "async" keyword while preserving function structure

Pattern: "(import\\s+\\{.*?\\}\\s+from\\s+['\"])(.*?)(['\"])"
Replacement: "\\1@/\\2\\3"
→ Updates import paths with @ prefix

Pattern: "(class\\s+)(\\w+)(\\s+extends\\s+)(\\w+)"
Replacement: "\\1New\\2\\3\\4"
→ Adds "New" prefix to class names
```

## Advanced Replacement Scenarios

### Configuration Updates
```
# Environment variable updates
Pattern: "DATABASE_URL=.*"
Replacement: "DATABASE_URL=new_database_connection_string"
→ Update configuration values

# JSON property updates
Pattern: "\"version\":\\s*\".*?\""
Replacement: "\"version\": \"2.0.0\""
→ Update JSON property values
```

### Code Refactoring
```
# Method signature updates
Pattern: "public (\\w+) (\\w+)\\((.*?)\\)"
Replacement: "public \\1 \\2(\\3) throws Exception"
→ Add exception handling to method signatures

# Variable renaming with type preservation
Pattern: "(\\w+)\\s+(oldVariableName)\\s*="
Replacement: "\\1 newVariableName ="
→ Rename variables while preserving types
```

### Framework Migration
```
# React class to functional component
Pattern: "class (\\w+) extends Component\\s*\\{.*?render\\(\\)\\s*\\{(.*?)\\}.*?\\}"
Replacement: "function \\1() {\\2}"
→ Convert class components to functional components

# API endpoint updates
Pattern: "app\\.(get|post|put|delete)\\s*\\(['\"](/api/v1/.*?)['\"]"
Replacement: "app.\\1('/api/v2\\2'"
→ Update API version in route definitions
```

## Error Handling and Troubleshooting

### No Matches Found
```
Error: "No matches found for regex 'pattern' in file 'filename'"

Troubleshooting:
- Check pattern syntax and escaping
- Verify pattern matches actual file content
- Use simpler pattern to test matching
- Check for case sensitivity issues
- Verify file contains expected content
```

### Multiple Occurrences Error
```
Error: "Regex 'pattern' matches N occurrences. Please revise to be more specific or enable allow_multiple_occurrences"

Solutions:
- Make pattern more specific to match only intended content
- Use backreferences to preserve context
- Set allow_multiple_occurrences=true if multiple replacements intended
- Break into multiple targeted replacements
```

### Invalid Regex Pattern
```
Error: "Invalid regular expression syntax"

Common issues:
- Unescaped special characters: ( ) { } [ ] . * + ? ^ $ | \
- Unclosed character classes: [abc (missing closing bracket)
- Invalid backreferences: \9 when only 3 groups captured
- Invalid escape sequences: \z (invalid escape character)

Fixes:
- Escape special characters: \\( \\) \\{ \\}
- Close character classes properly: [abc]
- Use valid backreferences: \1 \2 \3
- Use valid escape sequences: \\n \\t \\\\
```

### Replacement String Issues
```
Error: "Invalid replacement string"

Common problems:
- Invalid backreferences: \5 when only 2 groups captured
- Unescaped backslashes: \n instead of \\n for literal newline
- Special character conflicts in replacement strings

Solutions:
- Use valid backreference numbers: \1 \2 \3
- Escape backslashes properly: \\n \\t \\\\
- Test replacement strings with simple patterns first
```

## Best Practices

### 1. Design Flexible Patterns
```
✅ Use wildcards (.*?) for variable content
✅ Make patterns resilient to formatting changes
✅ Capture important parts with parentheses for backreferences
✅ Test patterns with multiple examples before applying

❌ Write overly specific patterns that break easily
❌ Ignore formatting variations in code
❌ Miss opportunities to use backreferences
❌ Apply patterns without testing on sample content
```

### 2. Handle Occurrences Appropriately
```
✅ Use allow_multiple_occurrences=true when replacing all instances
✅ Use allow_multiple_occurrences=false when expecting single replacement
✅ Design specific patterns to avoid unintended matches
✅ Plan for cases where no matches are found

❌ Allow multiple occurrences without considering impact
❌ Use overly broad patterns that match unintended content
❌ Ignore the possibility of no matches
❌ Fail to validate replacement scope and intent
```

### 3. Test and Validate Carefully
```
✅ Test regex patterns on sample content before applying
✅ Verify replacement strings produce expected results
✅ Check that backreferences work correctly
✅ Validate file content after replacement

❌ Apply complex patterns without testing
❌ Skip validation of replacement results
❌ Ignore potential unintended side effects
❌ Fail to check file integrity after changes
```

### 4. Use Appropriate Tools for the Task
```
✅ Use regex replacement for pattern-based changes
✅ Use symbol-level tools when working with code structures
✅ Use simple text replacement for exact string matches
✅ Choose the right tool based on change complexity

❌ Use regex for simple exact string replacements
❌ Use text replacement for complex pattern matching
❌ Ignore more appropriate symbol-level modification tools
❌ Over-complicate simple changes with complex regex
```

## Integration with Development Workflow

### Code Refactoring
```
1. Identify pattern for modification → Design appropriate regex pattern
2. Test pattern on sample content → Verify matching works correctly
3. Design replacement strategy → Plan backreferences and new content
4. Execute replacement → Apply changes with appropriate occurrence settings
5. Validate results → Check file content and functionality
```

### Configuration Updates
```
→ Use regex replacement for systematic configuration changes
→ Update environment variables and settings across files
→ Modify build configurations and deployment settings
→ Apply consistent changes to similar configuration patterns
```

### Framework Migration
```
→ Update import statements and module references
→ Modify API calls and method signatures
→ Convert between different code patterns and structures
→ Apply systematic changes for library or framework upgrades
```

This workflow replaces ReplaceRegexTool functionality for performing precise pattern-based text replacements in files using regular expressions.