# Read Memory

## Function Description (Replaces ReadMemoryTool)

When user requests to retrieve stored project-specific information from memory storage, execute the following workflow to access and return relevant knowledge:

## Step 1: Specify Memory Name
**Description**: Identify the memory file to read and validate its relevance
**Requirements**:
- Memory name must exist in the project memory store
- Information should be relevant to current task
- Avoid reading the same memory multiple times in one conversation

**Memory Name Examples**:
```
# Project configuration
Memory: "project_setup"
→ Read: Technology stack and configuration details

# API documentation
Memory: "api_endpoints"
→ Read: Available endpoints and their specifications

# Database schema
Memory: "database_schema"
→ Read: Table structures and relationships

# Development procedures
Memory: "deployment_process"
→ Read: Deployment steps and configuration
```

## Step 2: Validate Memory Existence
**Description**: Check if the requested memory exists before attempting to read
**Validation Process**:
- Verify memory exists in project memory store
- Check if memory name is correctly specified
- Ensure user has proper access permissions

**Validation Examples**:
```
# Memory exists
Request: "project_setup"
→ Status: ✅ Memory found
→ Action: Proceed with reading

# Memory not found
Request: "nonexistent_memory"
→ Status: ❌ Memory not found
→ Action: Return error message

# Memory name typo
Request: "projet_setup" (typo)
→ Status: ❌ Memory not found
→ Suggestion: Check available memories or correct spelling
```

## Step 3: Retrieve Memory Content
**Description**: Load and return the complete memory content
**Retrieval Process**:
- Load memory content from storage
- Maintain original markdown formatting
- Include all stored information
- Apply character limits if specified

**Content Handling**:
```
# Standard retrieval
→ Return: Complete memory content in markdown format
→ Preserve: Original structure and formatting
→ Include: All sections and examples

# With character limits
→ Check: Content length against limits
→ Truncate: If necessary with warning
→ Maintain: Readability of truncated content
```

## Step 4: Format and Return Results
**Description**: Present memory content in readable format with metadata
**Output Format**:
- Return complete memory content
- Preserve markdown formatting
- Include retrieval timestamp if needed
- Add context about memory purpose

**Standard Output Structure**:
```markdown
# Retrieved Memory: project_setup

[Complete memory content as stored, maintaining all formatting]

## Technology Stack
- **Python**: 3.9+
- **Web Framework**: FastAPI
- **Database**: PostgreSQL 13+

## Configuration
...

[Rest of memory content]
```

## Complete Workflow Examples

### Example 1: Read Project Setup Information
**Request**: "Read memory 'project_setup' to understand project configuration"

#### Step 1: Specify memory
```
Target memory: "project_setup"
Purpose: Understand project configuration
Relevance: High - needed for development tasks
```

#### Step 2: Validate existence
```
Check: Memory "project_setup" exists
Status: ✅ Found
Size: 2.5KB content
```

#### Step 3: Retrieve content
```
Action: Load complete memory content
Format: Preserve markdown structure
Content: Project configuration and tech stack details
```

#### Step 4: Expected output
```markdown
# Project Setup Information

## Technology Stack
- **Python**: 3.9+
- **Web Framework**: FastAPI
- **Database**: PostgreSQL 13+
- **ORM**: SQLAlchemy 1.4+
- **Caching**: Redis 6+
- **Containerization**: Docker & Docker Compose

## Development Environment
- **Package Manager**: Poetry
- **Code Formatting**: Black, isort
- **Linting**: flake8, mypy
- **Testing**: pytest with coverage

## Database Configuration
- **Host**: localhost (development)
- **Port**: 5432
- **Database Name**: myapp_dev
- **Migrations**: Alembic

## Key Dependencies
```
fastapi>=0.68.0
sqlalchemy>=1.4.0
alembic>=1.7.0
redis>=4.0.0
pytest>=6.0.0
```

## Environment Variables
- `DATABASE_URL`: PostgreSQL connection string
- `REDIS_URL`: Redis connection string
- `SECRET_KEY`: JWT signing key
```

### Example 2: Read API Documentation
**Request**: "Read memory 'api_endpoints' for API reference"

#### Step 1: Specify memory
```
Target memory: "api_endpoints"
Purpose: API development reference
Context: Working on new endpoint implementation
```

#### Step 2: Validate and retrieve
```
Memory status: ✅ Found
Content type: API documentation
Size: 3.2KB
```

#### Step 3: Expected output
```markdown
# API Endpoints Documentation

## Authentication Endpoints

### POST /auth/login
- **Purpose**: User authentication
- **Body**: `{"username": "string", "password": "string"}`
- **Response**: JWT token and user info
- **Status Codes**: 200 (success), 401 (invalid credentials)

### POST /auth/logout
- **Purpose**: Logout current user
- **Headers**: `Authorization: Bearer <token>`
- **Response**: Success message

## User Management

### GET /users/me
- **Purpose**: Get current user profile
- **Headers**: `Authorization: Bearer <token>`
- **Response**: User object

[Rest of API documentation...]
```

### Example 3: Read Development Procedures
**Request**: "Read memory 'deployment_process' for deployment guidance"

#### Step 1: Specify memory
```
Target memory: "deployment_process"
Purpose: Learn deployment procedures
Task context: Preparing for production deployment
```

#### Step 2: Validate and retrieve
```
Memory found: ✅ "deployment_process"
Content: Step-by-step deployment guide
Last updated: Recent
```

## Memory Categories and Use Cases

### Configuration Information
- **project_setup**: Technology stack and dependencies
- **environment_config**: Environment variables and settings
- **database_config**: Database connection and schema info

### Documentation
- **api_endpoints**: REST API documentation
- **architecture_overview**: System design and components
- **coding_standards**: Code style and conventions

### Procedures and Workflows
- **deployment_process**: Deployment steps and procedures
- **testing_strategy**: Testing approach and tools
- **code_review_process**: Code review guidelines

### Troubleshooting Knowledge
- **common_errors**: Frequent errors and solutions
- **debugging_procedures**: How to debug problems
- **performance_tips**: Performance optimization advice

## Best Practices

### 1. Check Relevance First
```
✅ Only read memories relevant to current task
✅ Consider memory name to understand content
✅ Avoid reading unrelated information

❌ Read all memories without purpose
❌ Read memories multiple times in same conversation
❌ Read irrelevant memories
```

### 2. Use Memory Content Effectively
```
✅ Apply information from memory to current task
✅ Reference specific sections as needed
✅ Combine memory info with current context

❌ Ignore memory content after reading
❌ Fail to apply relevant information
❌ Misinterpret memory content
```

### 3. Optimize Memory Usage
```
✅ Read memories when needed for task
✅ Choose specific memories based on name
✅ Use information to guide further actions

❌ Read memories speculatively
❌ Read all available memories at once
❌ Waste time with irrelevant memories
```

## Error Handling

### Memory Not Found
```
Error: "Memory 'memory_name' not found"
Solutions:
- Check available memories using list_memories
- Verify correct spelling of memory name
- Check if memory was deleted or never created
```

### Permission Denied
```
Error: "Access denied for memory 'memory_name'"
Solutions:
- Verify user has proper access permissions
- Check if memory is project-specific
- Ensure working in correct project context
```

### Content Too Large
```
Warning: "Memory content truncated due to size limits"
Solutions:
- Read memory in sections if possible
- Request specific parts of large memories
- Consider breaking large memories into smaller ones
```

## Integration with Development Workflow

### Before Starting Tasks
1. **Check available memories**: Use list_memories to see what's available
2. **Read relevant memories**: Get information needed for current task
3. **Apply knowledge**: Use memory content to guide implementation

### During Development
1. **Reference procedures**: Read process memories when needed
2. **Check configuration**: Read setup memories for environment info
3. **Follow standards**: Read coding standards and conventions

### When Stuck
1. **Read troubleshooting memories**: Look for common solutions
2. **Check debugging procedures**: Follow established debugging steps
3. **Review documentation**: Read API or architecture memories

## Common Reading Patterns

### Project Onboarding
```
1. Read "project_setup"        → Understand technology stack
2. Read "development_process"  → Learn workflow procedures
3. Read "coding_standards"     → Understand code conventions
4. Read "architecture_overview" → Understand system design
```

### Feature Development
```
1. Read "api_endpoints"        → Understand existing APIs
2. Read "database_schema"      → Understand data structures
3. Read "testing_strategy"     → Know how to test new features
```

### Troubleshooting
```
1. Read "common_errors"        → Check for known issues
2. Read "debugging_procedures" → Follow debugging steps
3. Read "performance_tips"     → Optimize if performance issue
```

### Deployment
```
1. Read "deployment_process"   → Follow deployment steps
2. Read "environment_config"   → Set up environment correctly
3. Read "testing_strategy"     → Run proper tests before deploy
```

This workflow replaces ReadMemoryTool functionality for retrieving stored project-specific knowledge and information.