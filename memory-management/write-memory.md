# Write Memory

## Function Description (Replaces WriteMemoryTool)

When user requests to store project-specific information for future reference, execute the following workflow to save knowledge in memory storage:

## Step 1: Define Memory Content
**Description**: Specify the information to store and memory name
**Requirements**:
- Memory name should be meaningful and descriptive
- Content should be in markdown format
- Information should be project-specific and useful for future tasks
- Content length should be reasonable

**Memory Categories**:
```
# Project Setup Information
Memory: "project_setup"
Content: Technology stack, dependencies, configuration

# API Documentation
Memory: "api_endpoints"
Content: Available endpoints, request/response formats

# Database Schema
Memory: "database_schema"
Content: Table structures, relationships, migrations

# Development Workflow
Memory: "development_process"
Content: Build process, testing procedures, deployment
```

## Step 2: Format Content Structure
**Description**: Structure information in clear, reusable format
**Content Guidelines**:
- Use markdown formatting for readability
- Include examples and code snippets
- Organize information hierarchically
- Add relevant context and explanations

**Content Structure Example**:
```markdown
# Project Setup Information

## Technology Stack
- **Python**: 3.9+
- **Web Framework**: FastAPI
- **Database**: PostgreSQL 13+
- **ORM**: SQLAlchemy 1.4+

## Dependencies
```
fastapi>=0.68.0
sqlalchemy>=1.4.0
alembic>=1.7.0
```

## Configuration
- Database URL: Set via DATABASE_URL environment variable
- Secret Key: Set via SECRET_KEY environment variable
```

## Step 3: Validate Content Length
**Description**: Ensure content is within acceptable limits
**Validation Rules**:
- Content should not exceed maximum character limit
- Break large content into multiple memories if needed
- Focus on essential information
- Remove redundant or outdated information

**Content Management**:
```
# Appropriate content size
✅ Focused, specific information
✅ Essential details only
✅ Well-organized structure

# Content too large
❌ Entire documentation copied
❌ Redundant information
❌ Unstructured data dump
```

## Step 4: Save Memory
**Description**: Store the memory with descriptive name
**Storage Process**:
- Use meaningful memory name
- Save content in markdown format
- Confirm successful storage
- Make available for future retrieval

**Memory Naming Conventions**:
```
# Good memory names
✅ "project_setup"           → Clear purpose
✅ "api_authentication"      → Specific topic
✅ "database_schema"         → Well-defined scope
✅ "testing_strategy"        → Focused area

# Poor memory names
❌ "notes"                   → Too vague
❌ "misc_info"              → Not descriptive
❌ "temp_data"              → Unclear purpose
```

## Complete Workflow Examples

### Example 1: Store Project Setup Information
**Request**: "Store project setup information including technology stack and configuration"

#### Step 1: Define content
```
Memory name: "project_setup"
Content type: Project configuration and tech stack
Format: Markdown with sections
```

#### Step 2: Structure content
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

#### Step 3: Save memory
```
Action: Store content with name "project_setup"
Result: Memory saved successfully
```

### Example 2: Store API Documentation
**Request**: "Store API endpoints documentation for reference"

#### Step 1: Define content
```
Memory name: "api_endpoints"
Content type: API documentation
Focus: Endpoints, parameters, responses
```

#### Step 2: Structure content
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

### PUT /users/me
- **Purpose**: Update user profile
- **Headers**: `Authorization: Bearer <token>`
- **Body**: User update data
- **Response**: Updated user object

## Error Responses
- **400**: Bad Request - Invalid input data
- **401**: Unauthorized - Missing or invalid token
- **403**: Forbidden - Insufficient permissions
- **404**: Not Found - Resource doesn't exist
- **500**: Internal Server Error - Server error
```

### Example 3: Store Database Schema
**Request**: "Store database schema information for development reference"

#### Step 1: Define content
```
Memory name: "database_schema"
Content type: Database structure documentation
Focus: Tables, relationships, constraints
```

#### Step 2: Structure content
```markdown
# Database Schema Documentation

## Tables Overview

### users
- **Purpose**: Store user account information
- **Primary Key**: id (serial)
- **Indexes**: email (unique), username (unique)

```sql
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    username VARCHAR(50) UNIQUE NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    password_hash VARCHAR(255) NOT NULL,
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    is_active BOOLEAN DEFAULT TRUE,
    is_admin BOOLEAN DEFAULT FALSE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### orders
- **Purpose**: Store customer orders
- **Primary Key**: id (serial)
- **Foreign Keys**: user_id → users(id)

```sql
CREATE TABLE orders (
    id SERIAL PRIMARY KEY,
    user_id INTEGER NOT NULL REFERENCES users(id),
    total_amount DECIMAL(10,2) NOT NULL,
    status VARCHAR(20) DEFAULT 'pending',
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

## Relationships
- **users** ← **orders** (one-to-many)
- **orders** ← **order_items** (one-to-many)
- **products** ← **order_items** (one-to-many)
```

## Memory Categories

### Technical Documentation
- **project_setup**: Technology stack and configuration
- **database_schema**: Database structure and relationships
- **api_endpoints**: REST API documentation
- **architecture_overview**: System design and components

### Process Documentation
- **deployment_process**: How to deploy the application
- **testing_strategy**: Testing approach and tools
- **code_review_process**: Code review instructions
- **release_process**: How to create releases

### Development Information
- **coding_standards**: Code style and conventions
- **naming_conventions**: How to name variables, functions, classes
- **error_handling**: Error handling patterns
- **logging_strategy**: How to log information

### Troubleshooting Knowledge
- **common_errors**: Frequent errors and solutions
- **performance_tips**: Performance optimization advice
- **debugging_procedures**: How to debug problems
- **environment_issues**: Environment-specific problems

## Best Practices

### 1. Use Descriptive Names
```
✅ "authentication_flow"     → Clear purpose
✅ "database_migration_process" → Specific procedure
✅ "testing_unit_test_setup" → Focused area

❌ "notes"                   → Too vague
❌ "stuff"                   → Not descriptive
❌ "random_info"            → Unclear content
```

### 2. Structure Content Well
```markdown
# Main Topic

## Overview
Brief description

## Detailed Sections
### Subsection 1
Specific information

### Subsection 2
More details

## Examples
```code
example here
```

## References
Additional information
```

### 3. Focus on Useful Information
```
✅ Information needed for future tasks
✅ Project-specific knowledge
✅ Procedures and processes
✅ Configuration details

❌ Temporary notes
❌ Personal reminders
❌ Irrelevant information
❌ Outdated content
```

### 4. Keep Content Current
```
✅ Update when information changes
✅ Remove outdated information
✅ Add new discoveries
✅ Maintain accuracy

❌ Let memories become stale
❌ Keep conflicting information
❌ Ignore updates
```

## Common Use Cases

### 1. Project Onboarding
Store essential project information for new team members or future reference

### 2. Configuration Documentation
Save important configuration details that are frequently referenced

### 3. Process Documentation
Record development, testing, and deployment procedures

### 4. Troubleshooting Knowledge
Store solutions to common problems and debugging procedures

## Error Handling

### Content Too Long
```
Error: "Content for memory_name is too long"
Solution: Break content into smaller, focused memories
```

### Invalid Memory Name
```
Error: "Invalid memory name format"
Solution: Use descriptive, valid identifier names
```

### Storage Failed
```
Error: "Failed to save memory"
Solution: Check memory system status and retry
```

## Integration with Development Workflow

### When to Create Memories
1. **After project setup**: Store configuration and setup information
2. **During development**: Save important discoveries and procedures
3. **After problem solving**: Store solutions for future reference
4. **During documentation**: Save structured information

### Memory Lifecycle
1. **Create**: Store new information
2. **Update**: Modify existing memories when information changes
3. **Reference**: Read memories when needed for tasks
4. **Delete**: Remove outdated or incorrect memories

This workflow replaces WriteMemoryTool functionality for storing project-specific knowledge and information.