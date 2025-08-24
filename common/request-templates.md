# Request Templates

## Overview
This document provides standardized templates for common Flow-Bento development requests. These templates ensure consistent and accurate communication when requesting code analysis operations.

## Template Format Convention

All requests follow this standardized format:
```
"[ACTION] [TARGET] [SCOPE] [OPTIONS]"
```

- **ACTION**: What operation to perform (Find, Read, Activate, etc.)
- **TARGET**: What to operate on (symbol name, file path, etc.)
- **SCOPE**: Where to perform the operation (project, directory, file)
- **OPTIONS**: Additional parameters and filters

## Symbol Analysis Templates

### Find Symbol Definitions

#### Basic Symbol Search
```
Template: "Find [SYMBOL_TYPE] named [NAME] in [SCOPE]"
Examples:
- "Find class named User in entire project"
- "Find method named login in src/auth/ directory"
- "Find function named process_data in utils.py file"
```

#### Symbol Search with Filters
```
Template: "Find [SYMBOL_TYPE] named [NAME] in [SCOPE], [FILTER_OPTIONS]"
Examples:
- "Find methods starting with get_ in models/ directory, exclude tests"
- "Find classes containing User in entire project, with children"
- "Find functions in src/ directory, with source code"
```

#### Advanced Pattern Search
```
Template: "Find [SYMBOL_TYPE] matching [PATTERN] in [SCOPE], [DETAIL_LEVEL]"
Examples:
- "Find methods matching validate_* in entire project, metadata only"
- "Find classes in User hierarchy in models/ directory, with full details"
- "Find constructors in Controller classes in controllers/ directory"
```

### Find Symbol References

#### Basic Reference Search
```
Template: "Find all references to [SYMBOL] in [SOURCE_FILE]"
Examples:
- "Find all references to login method in src/auth/user.py"
- "Find all references to User class in src/models/user.py"
- "Find all references to DATABASE_URL in src/config/settings.py"
```

#### Reference Search with Context
```
Template: "Find all references to [SYMBOL] in [SOURCE_FILE], showing [CONTEXT_LEVEL]"
Examples:
- "Find all references to save method in src/models/base.py, showing extended context"
- "Find all references to Config class in src/config/app.py, showing minimal context"
- "Find all references to authenticate in src/auth/service.py, showing standard context"
```

#### Filtered Reference Search
```
Template: "Find all references to [SYMBOL] in [SOURCE_FILE], [FILTER_OPTIONS]"
Examples:
- "Find all references to User in src/models/user.py, exclude tests"
- "Find all references to send_email in src/utils/email.py, methods only"
- "Find all references to API_KEY in src/config/env.py, exclude imports"
```

## File Operations Templates

### Read File Content

#### Complete File Reading
```
Template: "Read file [FILE_PATH] with [SCOPE_OPTION]"
Examples:
- "Read file src/main.py with entire file"
- "Read file README.md with max 2000 chars"
- "Read file package.json with unlimited length"
```

#### Partial File Reading
```
Template: "Read file [FILE_PATH] with [LINE_RANGE]"
Examples:
- "Read file src/service.py with lines 50-100"
- "Read file src/models/user.py with lines 0-30"
- "Read file src/utils/helpers.py with first 50 lines"
```

### List Directory Contents

#### Basic Directory Listing
```
Template: "List contents of [DIRECTORY_PATH] with [RECURSION_OPTION]"
Examples:
- "List contents of src/ directory with recursive search"
- "List contents of . with non-recursive search"
- "List contents of tests/ directory with recursive search"
```

#### Directory Listing with Limits
```
Template: "List contents of [DIRECTORY_PATH] with [RECURSION_OPTION], [SIZE_LIMIT]"
Examples:
- "List contents of src/ directory with recursive search, max 3000 chars"
- "List contents of docs/ directory with non-recursive search, unlimited"
```

### Find Files

#### File Pattern Search
```
Template: "Find files matching [PATTERN] in [DIRECTORY]"
Examples:
- "Find files matching *.py in src/ directory"
- "Find files matching test_*.py in tests/ directory"
- "Find files matching *.json in . directory"
```

## Project Management Templates

### Project Activation

#### Activate by Name
```
Template: "Activate project [PROJECT_NAME] and show [INFO_LEVEL]"
Examples:
- "Activate project web-frontend and show full overview"
- "Activate project api-backend and show basic info"
- "Activate project flow-bento-tools and show project details"
```

#### Activate by Path
```
Template: "Activate project [PROJECT_PATH] and show [INFO_LEVEL]"
Examples:
- "Activate project /home/user/my-app and show full overview"
- "Activate project . and show memories list"
- "Activate project ../other-project and show tools list"
```

## Memory Management Templates

### Write Memory
```
Template: "Write memory [MEMORY_NAME] with content: [CONTENT]"
Examples:
- "Write memory project_setup with content: Database uses PostgreSQL with SQLAlchemy ORM"
- "Write memory api_endpoints with content: REST API with /users, /auth, /data endpoints"
- "Write memory testing_approach with content: Uses pytest with fixtures and mock patterns"
```

### Read Memory
```
Template: "Read memory [MEMORY_NAME]"
Examples:
- "Read memory project_setup"
- "Read memory api_documentation"
- "Read memory deployment_notes"
```

### List Memories
```
Template: "List all available memories"
Example:
- "List all available memories"
```

## Command Execution Templates

### Execute Shell Commands
```
Template: "Execute command [COMMAND] in [WORKING_DIRECTORY]"
Examples:
- "Execute command npm test in . directory"
- "Execute command python -m pytest in tests/ directory"
- "Execute command ls -la in src/ directory"
```

## Workflow Management Templates

### Project Onboarding
```
Template: "Check onboarding status" or "Perform project onboarding"
Examples:
- "Check onboarding status"
- "Perform project onboarding"
```

### Task Reflection
```
Template: "Think about [REFLECTION_TYPE]"
Examples:
- "Think about collected information"
- "Think about task adherence"
- "Think about whether task is complete"
```

## Complex Operation Templates

### Code Analysis Workflow

#### Understanding New Code
```
Sequence:
1. "Activate project [NAME] and show full overview"
2. "List contents of src/ directory with recursive search"
3. "Get symbols overview for [MAIN_FILE]"
4. "Find class [MAIN_CLASS] in [FILE], with children"
5. "Read file [FILE] with lines [X-Y]"
```

#### Impact Analysis
```
Sequence:
1. "Find symbol [TARGET_SYMBOL] in [FILE], with source code"
2. "Find all references to [TARGET_SYMBOL] in [FILE]"
3. "Read file [DEPENDENT_FILE] with lines around references"
4. "Think about collected information"
```

#### Debugging Workflow
```
Sequence:
1. "Find method [ERROR_METHOD] in [FILE], with source code"
2. "Find all references to [ERROR_METHOD] in [FILE]"
3. "Read file [CALLER_FILE] with extended context around calls"
4. "Check related symbols in same class"
```

## Parameter Mapping Reference

### Common Mappings

#### Symbol Types → include_kinds
- `"class"` → `[5]`
- `"method"` → `[6]`
- `"function"` → `[12]`
- `"variable"` → `[13]`
- `"constant"` → `[14]`
- `"constructor"` → `[9]`

#### Detail Levels → Tool Parameters
- `"metadata only"` → `include_body=False, depth=0`
- `"with children"` → `depth=1, include_body=False`
- `"with source code"` → `include_body=True`
- `"full details"` → `depth=1, include_body=True`

#### Context Levels → Context Size
- `"minimal context"` → 1-2 lines around reference
- `"standard context"` → 3-5 lines around reference
- `"extended context"` → 7-10 lines around reference

#### Scope Options → relative_path
- `"entire project"` → `""`
- `"src/ directory"` → `"src/"`
- `"specific file"` → `"path/to/file.py"`

## Request Validation Checklist

Before submitting a request, ensure:

### Required Elements
- [ ] Action verb is clear (Find, Read, Activate, etc.)
- [ ] Target is specified (symbol name, file path, etc.)
- [ ] Scope is defined (where to operate)

### Optional Elements
- [ ] Filters are appropriate for the task
- [ ] Detail level matches information needs
- [ ] Output limits are reasonable

### Common Mistakes to Avoid
- ❌ Vague requests: "Find stuff in the code"
- ❌ Missing scope: "Find User class" (where?)
- ❌ Inappropriate filters: "Find methods, classes only"
- ❌ Unrealistic expectations: "Find all bugs in code"

### Good Request Examples
- ✅ "Find class named UserService in src/services/ directory, with children"
- ✅ "Find all references to login method in src/auth/user.py, exclude tests"
- ✅ "Read file src/main.py with lines 1-50"
- ✅ "Activate project web-app and show project details"

This template system ensures consistent, clear, and effective communication with Flow-Bento development tools for all code analysis and manipulation tasks.