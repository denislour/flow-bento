# List Memories

## Function Description (Replaces ListMemoriesTool)

When user requests to see available memories in the project-specific memory store, execute the following workflow to display all stored memories:

## Step 1: Access Memory Store
**Description**: Connect to the project-specific memory storage system
**Requirements**:
- Access project memory store
- Enumerate all available memory files
- Check accessibility and permissions

**Access Process**:
```
# Memory store location
→ Project-specific storage directory
→ Contains all saved memories for current project
→ Organized by memory names and creation dates

# Permission verification
→ Verify read access to memory store
→ Check project context is active
→ Ensure proper authentication
```

## Step 2: Enumerate Available Memories
**Description**: Scan memory store to find all available memory files
**Enumeration Process**:
- Scan all memory files in storage
- Extract memory names and metadata
- Collect creation and modification timestamps
- Calculate memory sizes and content summaries

**Memory Information Collected**:
```
# Basic memory data
- Memory name (identifier)
- File size in bytes/KB
- Creation timestamp
- Last modification timestamp

# Content metadata
- Content type (configuration, documentation, procedures)
- Brief description if available
- Memory category/topic
```

## Step 3: Organize Memory List
**Description**: Structure memory information for easy browsing
**Organization Principles**:
- Sort alphabetically by memory name
- Group by categories if applicable
- Show most relevant information
- Include size and date information

**Sorting and Grouping**:
```
# Alphabetical sorting
→ Order memories A-Z by name
→ Easy to find specific memories
→ Consistent presentation

# Optional categorization
→ Configuration memories
→ Documentation memories
→ Procedure memories
→ Troubleshooting memories
```

## Step 4: Format Output as JSON
**Description**: Present memory list in structured JSON format
**Output Format**:
- JSON array of memory objects
- Include name, size, and timestamp information
- Maintain compatibility with memory reading tools
- Provide clear and parseable structure

**Standard JSON Structure**:
```json
[
  "memory_name_1",
  "memory_name_2",
  "memory_name_3"
]
```

**Extended JSON Structure (if metadata available)**:
```json
[
  {
    "name": "project_setup",
    "size": "2.5KB",
    "created": "2024-01-15T10:30:00Z",
    "modified": "2024-01-20T14:45:00Z",
    "category": "configuration"
  },
  {
    "name": "api_endpoints",
    "size": "3.2KB", 
    "created": "2024-01-16T09:15:00Z",
    "modified": "2024-01-18T16:20:00Z",
    "category": "documentation"
  }
]
```

## Complete Workflow Examples

### Example 1: List All Available Memories
**Request**: "Show me all available memories in the project"

#### Step 1: Access memory store
```
Action: Connect to project-specific memory storage
Project: Current active project
Location: Project memory directory
```

#### Step 2: Scan for memories
```
Found memories:
- project_setup (2.5KB)
- api_endpoints (3.2KB)
- database_schema (1.8KB)
- deployment_process (2.1KB)
- coding_standards (1.2KB)
```

#### Step 3: Expected output
```json
[
  "api_endpoints",
  "coding_standards", 
  "database_schema",
  "deployment_process",
  "project_setup"
]
```

### Example 2: List Memories with Detailed Information
**Request**: "List memories with metadata information"

#### Step 1: Access and enumerate
```
Memory store: ✅ Accessible
Total memories: 8
Storage usage: 15.3KB
```

#### Step 2: Collect detailed metadata
```
Memories with details:
1. api_endpoints - 3.2KB - API documentation
2. coding_standards - 1.2KB - Development guidelines  
3. common_errors - 2.0KB - Troubleshooting guide
4. database_schema - 1.8KB - Database structure
5. deployment_process - 2.1KB - Deployment procedures
6. environment_config - 1.5KB - Environment setup
7. project_setup - 2.5KB - Technology stack
8. testing_strategy - 1.0KB - Testing procedures
```

#### Step 3: Formatted JSON output
```json
[
  "api_endpoints",
  "coding_standards",
  "common_errors", 
  "database_schema",
  "deployment_process",
  "environment_config",
  "project_setup",
  "testing_strategy"
]
```

### Example 3: Empty Memory Store
**Request**: "List available memories"

#### Step 1: Access memory store
```
Memory store: ✅ Accessible
Status: Empty - no memories found
```

#### Step 2: Expected output
```json
[]
```

#### Step 3: Additional information
```
Message: "No memories available. Consider performing onboarding or creating project documentation memories."
```

## Memory Categories and Organization

### Configuration Memories
- **project_setup**: Technology stack and dependencies
- **environment_config**: Environment variables and settings
- **database_config**: Database connection information
- **build_config**: Build and compilation settings

### Documentation Memories  
- **api_endpoints**: REST API documentation
- **architecture_overview**: System design documentation
- **component_guide**: Component usage and integration
- **database_schema**: Database structure and relationships

### Process Memories
- **deployment_process**: Deployment procedures and steps
- **testing_strategy**: Testing approach and procedures
- **code_review_process**: Code review guidelines
- **release_process**: Release management procedures

### Troubleshooting Memories
- **common_errors**: Frequent errors and solutions
- **debugging_procedures**: Debugging workflows
- **performance_tips**: Performance optimization advice
- **environment_issues**: Environment-specific problems

## Use Cases

### 1. Project Onboarding
**Scenario**: New team member or starting work on project
**Process**:
```
1. List memories → See what documentation exists
2. Identify key memories → project_setup, coding_standards
3. Read relevant memories → Understand project context
4. Begin development → With proper background knowledge
```

### 2. Task Planning
**Scenario**: Starting a new development task
**Process**:
```
1. List memories → Check available knowledge
2. Identify relevant memories → Based on task type
3. Read specific memories → Get needed information
4. Execute task → With proper guidance
```

### 3. Knowledge Management
**Scenario**: Managing project documentation
**Process**:
```
1. List memories → See current documentation
2. Identify gaps → Missing documentation areas
3. Create new memories → Fill knowledge gaps
4. Maintain existing → Update outdated information
```

### 4. Troubleshooting Support
**Scenario**: Encountering problems during development
**Process**:
```
1. List memories → Check troubleshooting resources
2. Find relevant memories → common_errors, debugging_procedures
3. Read solutions → Apply known fixes
4. Document new solutions → Create new memories if needed
```

## Best Practices

### 1. Regular Memory Inventory
```
✅ Periodically list memories to understand available knowledge
✅ Check for outdated or irrelevant memories
✅ Identify gaps in documentation
✅ Plan memory creation and updates

❌ Never check available memories
❌ Assume specific memories exist
❌ Work without understanding available resources
```

### 2. Memory Organization
```
✅ Use consistent naming conventions
✅ Group related memories logically
✅ Keep memory purposes clear and distinct
✅ Maintain reasonable memory sizes

❌ Use unclear or inconsistent names
❌ Create overlapping or duplicate memories
❌ Mix unrelated information in memories
```

### 3. Efficient Memory Usage
```
✅ List memories before reading to understand options
✅ Choose specific memories based on current needs
✅ Use memory list to guide development workflow
✅ Plan memory creation based on gaps

❌ Read memories randomly without checking list
❌ Miss useful memories due to poor awareness
❌ Create duplicate memories without checking existing ones
```

## Integration with Development Workflow

### Project Initialization
1. **List memories**: Check if project has existing documentation
2. **Assess completeness**: Identify what documentation exists
3. **Plan onboarding**: Create missing essential memories
4. **Begin development**: With full knowledge of available resources

### Daily Development
1. **Check available memories**: Quick list to see options
2. **Read relevant memories**: Get information for current task
3. **Work with guidance**: Use memory information to guide development
4. **Update memories**: Add new knowledge discovered during work

### Problem Solving
1. **List memories**: Check for troubleshooting resources
2. **Find relevant help**: Identify memories that might contain solutions
3. **Read solutions**: Apply known fixes and procedures
4. **Document new findings**: Create memories for new solutions

### Project Maintenance
1. **Audit memories**: Regular listing to assess documentation
2. **Identify outdated content**: Find memories needing updates
3. **Plan improvements**: Create strategy for better documentation
4. **Maintain quality**: Keep memories current and useful

## Error Handling

### Memory Store Inaccessible
```
Error: "Cannot access memory store"
Solutions:
- Verify project is activated
- Check file system permissions
- Ensure proper project context
```

### Empty Memory Store
```
Result: [] (empty array)
Guidance:
- Consider performing project onboarding
- Create essential project memories
- Document key project information
```

### Permission Issues
```
Error: "Insufficient permissions for memory store"
Solutions:
- Check project access permissions
- Verify user authentication
- Contact project administrator
```

## Memory Management Tips

### Memory Naming Best Practices
```
✅ "project_setup"           → Clear, descriptive
✅ "api_authentication"      → Specific topic focus
✅ "database_migration_guide" → Detailed purpose
✅ "common_deployment_errors" → Specific problem area

❌ "notes"                   → Too vague
❌ "misc"                    → Unclear content
❌ "temp_info"              → Temporary nature unclear
❌ "stuff_about_apis"       → Informal, unclear
```

### Memory Content Guidelines
```
✅ Focus on specific topics or procedures
✅ Keep information current and accurate
✅ Use clear markdown formatting
✅ Include examples and practical guidance

❌ Mix unrelated topics in one memory
❌ Include outdated or incorrect information
❌ Use poor formatting or structure
❌ Provide vague or theoretical content only
```

This workflow replaces ListMemoriesTool functionality for discovering and managing available project memories.