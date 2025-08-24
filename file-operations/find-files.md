# Find Files

## Function Description (Replaces FindFilesTool)

When user requests to find files based on patterns, names, or paths, execute the following workflow to locate files within the project structure:

## Step 1: Define File Search Parameters
**Description**: Specify the search criteria for finding files in the project
**Search Parameter Types**:
- File name patterns (exact names, wildcards, glob patterns)
- Directory scope (entire project, specific directories, subdirectories)
- File type filters (extensions, file categories)
- Path pattern matching (relative paths, directory patterns)

**Search Pattern Examples**:
```
# Exact file names
Pattern: "config.json"
→ Find: Exact file named config.json

# Wildcard patterns
Pattern: "*.py"
→ Find: All Python files
Pattern: "test_*.py"
→ Find: All Python test files starting with "test_"

# Glob patterns
Pattern: "**/*.js"
→ Find: All JavaScript files in any subdirectory
Pattern: "src/**/*.java"
→ Find: All Java files under src directory

# Directory patterns
Pattern: "**/models/**"
→ Find: All files in any models directory
Pattern: "src/components/*.tsx"
→ Find: All TypeScript React components
```

## Step 2: Configure Search Scope and Filters
**Description**: Set search boundaries and apply appropriate filters
**Scope Configuration**:
- **Entire project**: Search all directories and files
- **Specific directory**: Limit search to directory tree
- **Multiple directories**: Search in specified directory list
- **Depth limitation**: Control how deep to search in subdirectories

**Filter Options**:
```
# File type filtering
→ Include specific extensions (.py, .js, .java, .md)
→ Exclude certain file types (.pyc, .class, .log)
→ Focus on source code files only
→ Include or exclude configuration files

# Directory filtering
→ Exclude common ignore patterns (node_modules, .git, __pycache__)
→ Include only source directories (src, lib, app)
→ Exclude build and output directories (build, dist, target)
→ Respect .gitignore patterns

# File size and date filtering
→ Filter by file size (small config files, large data files)
→ Filter by modification date (recent changes, old files)
→ Include or exclude empty files
```

## Step 3: Execute File Search Operation
**Description**: Perform the file search with specified criteria
**Search Execution**:
- Traverse directory structure according to scope
- Apply pattern matching to file names and paths
- Apply filters to narrow down results
- Collect matching file paths and metadata

**Search Optimization**:
```
# Efficient search strategies
→ Use indexed file systems when available
→ Parallel directory traversal for large projects
→ Early termination for common patterns
→ Cache frequently accessed directory structures

# Pattern matching optimization
→ Compile regex patterns for reuse
→ Use efficient glob implementations
→ Optimize wildcard matching algorithms
→ Handle case-sensitivity appropriately
```

## Step 4: Format and Return Results
**Description**: Process search results and format for easy consumption
**Result Processing**:
- Sort results by relevance, name, or path
- Group results by directory or file type
- Include file metadata (size, modification date)
- Limit results to manageable number

**Standard Result Format**:
```json
[
  {
    "relative_path": "src/models/user.py",
    "file_name": "user.py",
    "directory": "src/models",
    "file_size": 2048,
    "modified_date": "2024-01-15T10:30:00Z"
  },
  {
    "relative_path": "tests/test_user.py", 
    "file_name": "test_user.py",
    "directory": "tests",
    "file_size": 1024,
    "modified_date": "2024-01-14T16:45:00Z"
  }
]
```

## Complete Workflow Examples

### Example 1: Find Configuration Files
**Request**: "Find all configuration files in the project"

#### Step 1: Define search parameters
```
Search patterns:
- "*.json" (JSON configuration files)
- "*.yaml", "*.yml" (YAML configuration files)
- "*.ini", "*.cfg" (INI configuration files)
- "*.env" (Environment files)
- "config.*" (Files starting with config)
```

#### Step 2: Configure scope and filters
```
Search scope: Entire project
Include patterns:
- Configuration file extensions
- Common config file names (settings.py, app.config, etc.)

Exclude patterns:
- Build output directories
- node_modules and package caches
- Temporary and log directories
```

#### Step 3: Execute search
```
Search execution:
✅ Traverse all project directories
✅ Apply configuration file patterns
✅ Filter out build and cache directories
✅ Collect matching files with metadata
```

#### Step 4: Expected results
```json
[
  {
    "relative_path": "package.json",
    "file_name": "package.json",
    "directory": ".",
    "file_size": 1234
  },
  {
    "relative_path": "src/config/database.yml",
    "file_name": "database.yml", 
    "directory": "src/config",
    "file_size": 512
  },
  {
    "relative_path": ".env.example",
    "file_name": ".env.example",
    "directory": ".",
    "file_size": 256
  }
]
```

### Example 2: Find Test Files
**Request**: "Find all test files in the project"

#### Step 1: Define test file patterns
```
Test file patterns:
- "test_*.py" (Python test files)
- "*_test.py" (Python test files)
- "*.test.js" (JavaScript test files)
- "*.spec.js" (JavaScript spec files)
- "*Test.java" (Java test files)
```

#### Step 2: Configure test-specific scope
```
Search scope: Entire project with focus on test directories
Include directories:
- tests/
- test/
- src/test/
- spec/
- __tests__/

File pattern matching:
- Standard test file naming conventions
- Multiple programming languages
- Both unit and integration test patterns
```

#### Step 3: Expected test file results
```json
[
  {
    "relative_path": "tests/test_user_service.py",
    "file_name": "test_user_service.py",
    "directory": "tests",
    "file_size": 2048
  },
  {
    "relative_path": "src/components/__tests__/UserProfile.test.js",
    "file_name": "UserProfile.test.js",
    "directory": "src/components/__tests__",
    "file_size": 1536
  },
  {
    "relative_path": "src/test/java/UserServiceTest.java",
    "file_name": "UserServiceTest.java",
    "directory": "src/test/java",
    "file_size": 3072
  }
]
```

### Example 3: Find Files by Pattern in Specific Directory
**Request**: "Find all Python files in the models directory"

#### Step 1: Define specific search
```
Search pattern: "*.py"
Search scope: models directory and subdirectories
File type: Python source files only
Directory focus: models/ or **/models/
```

#### Step 2: Configure directory-specific search
```
Directory scope: 
- src/models/
- app/models/
- Any directory named "models"

Pattern matching:
- .py extension only
- Include all subdirectories under models
- Exclude __pycache__ and .pyc files
```

#### Step 3: Expected model file results
```json
[
  {
    "relative_path": "src/models/user.py",
    "file_name": "user.py",
    "directory": "src/models"
  },
  {
    "relative_path": "src/models/order.py",
    "file_name": "order.py", 
    "directory": "src/models"
  },
  {
    "relative_path": "src/models/auth/permission.py",
    "file_name": "permission.py",
    "directory": "src/models/auth"
  }
]
```

## File Search Strategies

### Pattern Matching Techniques
```
# Glob patterns (recommended)
"*.py"              → All Python files
"**/*.js"           → All JavaScript files recursively
"src/**/*.java"     → All Java files under src
"test_*.py"         → Python files starting with test_
"*Controller.java"  → Java files ending with Controller

# Regular expressions (advanced)
".*\\.py$"          → Python files (regex)
"test.*\\.js$"      → JavaScript test files
".*Config\\.(yml|yaml)$" → YAML config files

# Exact matching
"package.json"      → Specific file
"README.md"         → Exact filename
"Dockerfile"        → Exact match
```

### Directory Targeting
```
# Specific directories
"src/"              → Files in src directory
"tests/"            → Files in tests directory
"docs/"             → Files in docs directory

# Pattern-based directory matching
"**/models/**"      → Any models directory anywhere
"src/**/test/**"    → Test directories under src
"**/config/*"       → Config directories anywhere

# Multi-level patterns
"src/main/java/**/*.java"    → Java files in Maven structure
"app/components/**/*.tsx"    → React components
"lib/**/src/**/*.py"         → Python source in lib
```

### File Type Categories
```
# Source code files
Source: "*.py", "*.js", "*.java", "*.ts", "*.rb", "*.go"
Headers: "*.h", "*.hpp", "*.hxx"
Markup: "*.html", "*.jsx", "*.tsx", "*.vue"

# Configuration files
Config: "*.json", "*.yaml", "*.yml", "*.ini", "*.cfg"
Environment: "*.env", ".env.*"
Build: "*.gradle", "*.xml", "Makefile", "CMakeLists.txt"

# Documentation files
Docs: "*.md", "*.rst", "*.txt", "*.pdf"
README: "README*", "CHANGELOG*", "LICENSE*"

# Data files
Data: "*.csv", "*.json", "*.xml", "*.sql"
Images: "*.png", "*.jpg", "*.svg", "*.ico"
```

## Best Practices

### 1. Use Appropriate Search Patterns
```
✅ Use glob patterns for cross-platform compatibility
✅ Be specific with patterns to reduce false positives
✅ Use directory scoping to improve search efficiency
✅ Consider file naming conventions of the project

❌ Use overly broad patterns that return too many results
❌ Use platform-specific path separators in patterns
❌ Ignore project structure and naming conventions
❌ Use patterns that are too restrictive and miss files
```

### 2. Optimize Search Performance
```
✅ Limit search scope to relevant directories when possible
✅ Use exclude patterns to skip irrelevant directories
✅ Respect .gitignore and similar ignore patterns
✅ Use parallel search for large codebases

❌ Search entire filesystem unnecessarily
❌ Include build output and cache directories
❌ Ignore performance impact of broad searches
❌ Search binary and generated files unnecessarily
```

### 3. Handle Results Appropriately
```
✅ Sort results in logical order (alphabetical, by directory)
✅ Group results by file type or directory when helpful
✅ Limit results to manageable numbers
✅ Include relevant metadata for decision-making

❌ Return unsorted or randomly ordered results
❌ Overwhelm user with too many results
❌ Miss important files due to overly restrictive patterns
❌ Include irrelevant metadata that clutters results
```

### 4. Consider Project Context
```
✅ Understand project structure and conventions
✅ Use language-specific file patterns appropriately
✅ Respect project ignore patterns and exclusions
✅ Consider framework-specific directory structures

❌ Use generic patterns without project context
❌ Ignore project-specific naming conventions
❌ Include files that should be ignored
❌ Miss framework-specific file organization patterns
```

## Integration with Development Workflow

### Code Exploration
```
1. Find files by type → Understand project structure
2. Locate specific functionality → Find relevant source files
3. Identify configuration → Find config and setup files
4. Plan modifications → Understand file organization
```

### File Organization Analysis
```
→ Find all files of specific type for consistency analysis
→ Locate configuration files for environment setup
→ Identify test files for coverage analysis
→ Find documentation files for project understanding
```

### Build and Deployment
```
→ Find build configuration files (package.json, pom.xml)
→ Locate deployment scripts and configuration
→ Identify environment-specific configuration files
→ Find documentation and README files
```

## Error Handling

### No Files Found
```
Result: [] (empty array)
Possible causes:
- Pattern doesn't match any files
- Search scope is too narrow
- Files exist but are excluded by filters
- Pattern syntax is incorrect

Solutions:
- Broaden search pattern or scope
- Check pattern syntax and escaping
- Review exclude filters and ignore patterns
- Verify files exist with expected names
```

### Too Many Results
```
Warning: "Search returned excessive results"
Optimization strategies:
- Narrow search scope to specific directories
- Use more specific file patterns
- Add exclude filters for irrelevant files
- Break search into multiple targeted searches
```

### Permission Denied
```
Error: "Access denied to directory or file"
Solutions:
- Check file system permissions
- Verify user has read access to directories
- Skip restricted directories with appropriate filters
- Run with appropriate permissions if necessary
```

### Invalid Pattern
```
Error: "Invalid search pattern syntax"
Solutions:
- Check glob pattern syntax
- Escape special characters appropriately
- Use proper path separators for platform
- Test pattern with simple cases first
```

This workflow replaces FindFilesTool functionality for locating files using flexible patterns and filters within project structures.