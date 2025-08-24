# List Directory

## Function Description (Replaces ListDirTool)

When user requests to explore directory structure or list files and subdirectories, execute the following workflow to provide organized directory contents:

## Step 1: Specify Directory and Scan Parameters
**Description**: Define the directory to scan and scanning options
**Directory Specification**:
- Relative path from project root (use "." for project root)
- Directory must exist within the project
- Specify whether to scan recursively or only immediate contents
- Configure output limitations and filtering

**Scanning Options**:
```
# Directory targeting
→ "." for project root directory
→ "src" for source directory
→ "src/components" for specific subdirectory
→ "tests" for test directory

# Recursion options
→ Recursive: true - scan all subdirectories
→ Recursive: false - only immediate directory contents
→ Depth control for large directory trees
```

## Step 2: Validate Directory Existence
**Description**: Check that the specified directory exists and is accessible
**Validation Process**:
- Verify directory exists within project
- Check directory is not ignored by project ignore patterns
- Ensure proper access permissions
- Validate relative path format

**Validation Examples**:
```
# Valid directory paths
✅ "." → Project root
✅ "src" → Source directory  
✅ "src/components" → Components subdirectory
✅ "tests" → Test directory

# Invalid directory paths
❌ "../outside" → Outside project root
❌ "nonexistent" → Directory doesn't exist
❌ ".git" → Typically ignored directory
❌ "node_modules" → Usually ignored
```

## Step 3: Scan Directory Contents
**Description**: Traverse directory structure and collect file and directory information
**Scanning Process**:
- Traverse directory tree according to recursion setting
- Respect project ignore patterns (.gitignore, etc.)
- Separate directories from files
- Collect relative paths from project root

**Ignore Pattern Handling**:
```
# Commonly ignored patterns
→ .git/ directory and contents
→ node_modules/ and package dependencies
→ __pycache__/ and Python cache files
→ .DS_Store and system files
→ build/, dist/, target/ output directories
→ .env files and secrets
→ IDE-specific files (.vscode/, .idea/)

# Respect .gitignore patterns
→ Parse .gitignore file rules
→ Apply ignore patterns recursively
→ Exclude matching files and directories
→ Include only tracked or trackable files
```

## Step 4: Format Directory Listing Results
**Description**: Organize and format the directory contents for easy consumption
**Result Organization**:
- Separate directories and files for clarity
- Sort contents alphabetically
- Use relative paths from project root
- Apply output length limitations if needed

**Standard Result Format**:
```json
{
  "dirs": [
    "src",
    "src/components",
    "src/services", 
    "tests"
  ],
  "files": [
    "README.md",
    "package.json",
    "src/index.js",
    "src/components/App.js",
    "tests/app.test.js"
  ]
}
```

## Complete Workflow Examples

### Example 1: List Project Root Contents
**Request**: "List the contents of the project root directory"

#### Step 1: Specify directory
```
Directory: "." (project root)
Recursive: false (immediate contents only)
Include: Non-ignored files and directories
```

#### Step 2: Validate directory
```
Directory check: ✅ Project root exists
Permissions: ✅ Read access available
Ignore patterns: ✅ .gitignore rules loaded
```

#### Step 3: Scan contents
```
Scanning: Project root directory
Recursion: Disabled (immediate contents only)
Filtering: Apply ignore patterns
Collection: Separate dirs and files
```

#### Step 4: Expected results
```json
{
  "dirs": [
    "src",
    "tests", 
    "docs",
    "config"
  ],
  "files": [
    "README.md",
    "package.json",
    ".gitignore",
    "LICENSE"
  ]
}
```

### Example 2: Recursively List Source Directory
**Request**: "List all files and directories in the src directory recursively"

#### Step 1: Specify recursive scan
```
Directory: "src"
Recursive: true (include all subdirectories)
Scope: All source files and subdirectories
```

#### Step 2: Validate src directory
```
Directory: "src" exists ✅
Access: Read permissions ✅
Contents: Source code files and subdirectories
```

#### Step 3: Execute recursive scan
```
Scanning: src/ directory tree
Subdirectories: components/, services/, utils/
File types: .js, .ts, .jsx, .tsx, .css files
Filtering: Exclude build outputs and caches
```

#### Step 4: Expected recursive results
```json
{
  "dirs": [
    "src/components",
    "src/components/common",
    "src/services",
    "src/utils",
    "src/styles"
  ],
  "files": [
    "src/index.js",
    "src/App.js",
    "src/components/Header.js",
    "src/components/Footer.js", 
    "src/components/common/Button.js",
    "src/services/api.js",
    "src/services/auth.js",
    "src/utils/helpers.js",
    "src/styles/main.css"
  ]
}
```

### Example 3: List Test Directory Contents
**Request**: "Show me what's in the tests directory"

#### Step 1: Specify test directory
```
Directory: "tests"
Recursive: false (immediate contents)
Focus: Test files and test subdirectories
```

#### Step 2: Scan test directory
```
Directory: tests/ ✅
Content types: Test files, test data, test utilities
Organization: By test type or component
```

#### Step 3: Expected test directory results
```json
{
  "dirs": [
    "tests/unit",
    "tests/integration",
    "tests/fixtures"
  ],
  "files": [
    "tests/conftest.py",
    "tests/test_app.py",
    "tests/test_utils.py"
  ]
}
```

## Directory Exploration Strategies

### Project Structure Discovery
```
# Start with root overview
Directory: "." (recursive: false)
→ Understand top-level project organization
→ Identify main directories (src, tests, docs, config)
→ Plan deeper exploration of specific areas

# Explore specific areas
Directory: "src" (recursive: true)
→ Understand source code organization
→ Identify components, services, utilities
→ Map application architecture

# Analyze test structure  
Directory: "tests" (recursive: true)
→ Understand testing organization
→ Identify test categories and coverage
→ Plan test-related work
```

### Code Organization Analysis
```
# Component discovery
Directory: "src/components" (recursive: true)
→ Find all UI components
→ Understand component hierarchy
→ Identify reusable components

# Service layer exploration
Directory: "src/services" (recursive: true)
→ Discover business logic organization
→ Understand service dependencies
→ Map API and data access patterns

# Configuration analysis
Directory: "config" (recursive: true)
→ Find configuration files
→ Understand environment settings
→ Identify deployment configurations
```

### Framework-Specific Patterns
```
# React project structure
src/components/     → React components
src/hooks/         → Custom hooks
src/services/      → API services
src/utils/         → Utility functions
public/           → Static assets

# Node.js/Express structure
src/controllers/   → Route controllers
src/models/       → Data models
src/middleware/   → Express middleware
src/routes/       → Route definitions
config/          → Application configuration

# Python/Django structure
app/models/       → Django models
app/views/        → View functions/classes
app/templates/    → HTML templates
app/static/       → Static files
tests/           → Test files
```

## Best Practices

### 1. Start with Overview, Then Drill Down
```
✅ Begin with non-recursive root scan to understand structure
✅ Use recursive scans for specific areas of interest
✅ Focus exploration on relevant directories for current task
✅ Use directory structure to understand project organization

❌ Start with recursive scan of entire project
❌ Explore irrelevant directories unnecessarily
❌ Ignore overall project structure patterns
❌ Get lost in deep directory trees without context
```

### 2. Respect Project Ignore Patterns
```
✅ Trust ignore patterns to filter out irrelevant files
✅ Focus on source code and configuration files
✅ Exclude build outputs, dependencies, and temporary files
✅ Use ignore patterns to improve scan performance

❌ Try to access ignored directories
❌ Include build outputs and generated files in analysis
❌ Waste time on temporary or cache files
❌ Ignore project conventions for file organization
```

### 3. Use Appropriate Recursion Settings
```
✅ Use non-recursive for initial directory overview
✅ Use recursive for comprehensive area exploration
✅ Consider performance impact of deep recursive scans
✅ Focus recursive scans on specific areas of interest

❌ Always use recursive scanning unnecessarily
❌ Use non-recursive when deep exploration is needed
❌ Ignore performance implications of large recursive scans
❌ Scan entire project recursively without purpose
```

### 4. Understand Project Organization Patterns
```
✅ Learn project structure and naming conventions
✅ Identify framework-specific directory patterns
✅ Understand separation of concerns in directory structure
✅ Use structure knowledge to guide further exploration

❌ Ignore project organization patterns
❌ Miss framework-specific conventions
❌ Treat all directories as equivalent
❌ Fail to use structure for navigation planning
```

## Integration with Development Workflow

### Project Exploration
```
1. List root directory → Understand top-level organization
2. Identify key directories → Plan exploration strategy
3. Explore specific areas → Focus on relevant directories
4. Plan development work → Use structure knowledge for implementation
```

### File Discovery
```
→ Use directory listing to find relevant files
→ Understand file organization patterns
→ Identify configuration and setup files
→ Plan file reading and modification strategy
```

### Code Navigation
```
→ Use directory structure to understand codebase organization
→ Identify component and service boundaries
→ Find test files related to source code
→ Plan code exploration and modification approach
```

## Error Handling

### Directory Not Found
```
Error: "Directory not found: directory_name"
Solutions:
- Verify directory path is correct and relative to project root
- Check if directory was moved or renamed
- Ensure directory exists in current project state
- Use "." for project root if unsure about structure
```

### Permission Denied
```
Error: "Access denied to directory"
Solutions:
- Check file system permissions
- Ensure directory is not restricted
- Verify user has read access to project directories
- Check if directory is outside project boundaries
```

### Output Too Large
```
Warning: "Directory listing truncated due to size"
Solutions:
- Use non-recursive scanning for large directories
- Focus on specific subdirectories instead of entire tree
- Use file search tools for finding specific files in large structures
- Break exploration into smaller, targeted scans
```

### Empty Directory
```
Result: {"dirs": [], "files": []}
Interpretation:
- Directory exists but contains no non-ignored files
- All contents may be ignored by .gitignore patterns
- Directory may be empty or contain only system files
- Normal result for newly created or cleaned directories
```

## Common Directory Patterns

### Web Application Structure
```
src/                → Source code
  components/       → UI components
  services/         → Business logic
  utils/           → Utility functions
  styles/          → CSS and styling
tests/             → Test files
public/            → Static assets
docs/              → Documentation
config/            → Configuration files
```

### Backend Service Structure
```
src/               → Source code
  controllers/     → Request handlers
  models/          → Data models
  services/        → Business logic
  middleware/      → Request middleware
  routes/          → Route definitions
tests/             → Test files
config/            → Configuration
scripts/           → Utility scripts
```

### Library/Package Structure
```
src/               → Source code
lib/               → Compiled output
tests/             → Test files
docs/              → Documentation
examples/          → Usage examples
scripts/           → Build and utility scripts
```

This workflow replaces ListDirTool functionality for exploring and understanding project directory structure and file organization.