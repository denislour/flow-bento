# Check Onboarding Performed

## Function Description (Replaces CheckOnboardingPerformedTool)

When starting work on a project, execute the following workflow to determine if project onboarding has been completed and what information is already available:

## Step 1: Check Memory Store Status
**Description**: Examine the project memory store to determine onboarding status
**Requirements**:
- Check if any memories exist in the project memory store
- Determine completeness of project documentation
- Assess availability of essential project information

**Memory Store Analysis**:
```
# Check memory count
→ List all available memories
→ Count total memories found
→ Assess memory categories present

# Evaluate onboarding status
→ No memories = No onboarding performed
→ Few memories = Partial onboarding
→ Many memories = Complete onboarding
```

## Step 2: Analyze Available Memories
**Description**: If memories exist, categorize and evaluate their completeness
**Analysis Process**:
- List all available memory names
- Categorize memories by type (setup, documentation, procedures)
- Identify gaps in essential project information
- Determine memory relevance to current tasks

**Memory Categories Assessment**:
```
# Essential project memories
✅ project_setup - Technology stack and configuration
✅ development_process - Build and development workflow
✅ testing_strategy - Testing approach and tools
✅ deployment_process - Deployment procedures

# Documentation memories  
✅ api_endpoints - API documentation
✅ architecture_overview - System design
✅ database_schema - Database structure

# Process memories
✅ coding_standards - Code style guidelines
✅ code_review_process - Review procedures
```

## Step 3: Determine Onboarding Status
**Description**: Based on memory analysis, determine if onboarding is complete
**Status Categories**:
- **Not Performed**: No memories available, full onboarding needed
- **Partially Complete**: Some memories exist, additional onboarding may be needed
- **Complete**: Comprehensive memories available, ready to proceed

**Status Decision Logic**:
```
# No onboarding performed
→ Memory count: 0
→ Status: "Onboarding not performed yet"
→ Action: Recommend calling onboarding tool

# Onboarding completed
→ Memory count: > 0
→ Status: "Onboarding already performed" 
→ Action: List available memories for reference

# Partial onboarding
→ Memory count: > 0 but incomplete
→ Status: "Partial onboarding detected"
→ Action: Suggest completing missing documentation
```

## Step 4: Provide Guidance and Memory List
**Description**: Give appropriate guidance based on onboarding status
**Guidance Types**:
- **No Onboarding**: Direct to onboarding tool
- **Complete Onboarding**: List memories with usage guidance
- **Partial Onboarding**: Suggest completing missing areas

**Response Format**:
```
# If no onboarding
"Onboarding not performed yet (no memories available). You should perform onboarding by calling the `onboarding` tool before proceeding with the task."

# If onboarding complete
"The onboarding was already performed, below is the list of available memories. Do not read them immediately, just remember that they exist and that you can read them later, if it is necessary for the current task. Some memories may be based on previous conversations, others may be general for the current project. You should be able to tell which one you need based on the name of the memory.

[memory_list]"
```

## Complete Workflow Examples

### Example 1: No Onboarding Performed
**Request**: "Check if project onboarding has been completed"

#### Step 1: Check memory store
```
Action: List available memories
Result: [] (empty array)
Memory count: 0
```

#### Step 2: Analyze results
```
Status: No memories found
Assessment: No onboarding performed
Project knowledge: None available
```

#### Step 3: Determine status
```
Onboarding status: ❌ Not performed
Recommendation: Perform onboarding first
```

#### Step 4: Expected response
```
"Onboarding not performed yet (no memories available). You should perform onboarding by calling the `onboarding` tool before proceeding with the task."
```

### Example 2: Complete Onboarding
**Request**: "Check onboarding status for the project"

#### Step 1: Check memory store
```
Action: List available memories
Result: [
  "project_setup",
  "api_endpoints", 
  "database_schema",
  "deployment_process",
  "coding_standards",
  "testing_strategy"
]
Memory count: 6
```

#### Step 2: Analyze memories
```
Categories found:
✅ Configuration: project_setup
✅ Documentation: api_endpoints, database_schema
✅ Processes: deployment_process, testing_strategy
✅ Standards: coding_standards
```

#### Step 3: Determine status
```
Onboarding status: ✅ Complete
Available knowledge: Comprehensive
```

#### Step 4: Expected response
```
"The onboarding was already performed, below is the list of available memories.
Do not read them immediately, just remember that they exist and that you can read them later, if it is necessary for the current task.
Some memories may be based on previous conversations, others may be general for the current project.
You should be able to tell which one you need based on the name of the memory.

[
  "api_endpoints",
  "coding_standards",
  "database_schema", 
  "deployment_process",
  "project_setup",
  "testing_strategy"
]"
```

### Example 3: Partial Onboarding
**Request**: "Check if onboarding is complete"

#### Step 1: Check memory store
```
Action: List available memories
Result: ["project_setup", "database_schema"]
Memory count: 2
```

#### Step 2: Analyze completeness
```
Available memories:
✅ project_setup - Basic project info
✅ database_schema - Database structure

Missing memories:
❌ api_endpoints - API documentation
❌ deployment_process - Deployment procedures  
❌ testing_strategy - Testing approach
```

#### Step 3: Expected response
```
"Partial onboarding detected. The following memories are available:

[
  "database_schema",
  "project_setup"
]

Consider creating additional memories for:
- API endpoints documentation
- Deployment procedures
- Testing strategy
- Coding standards"
```

## Onboarding Assessment Criteria

### Essential Project Memories
```
# Core Configuration
project_setup          → Technology stack, dependencies
environment_config      → Environment variables, settings
build_config           → Build and compilation configuration

# Development Process
development_process     → Development workflow and procedures
coding_standards       → Code style and conventions
testing_strategy       → Testing approach and tools
code_review_process    → Code review guidelines

# Documentation
api_endpoints          → API documentation and specifications
architecture_overview  → System design and components
database_schema        → Database structure and relationships

# Operations
deployment_process     → Deployment procedures and configuration
monitoring_setup       → Monitoring and logging configuration
troubleshooting_guide  → Common issues and solutions
```

### Memory Quality Assessment
```
# Good onboarding indicators
✅ Multiple memory categories covered
✅ Essential project information documented
✅ Process and procedure memories present
✅ Recent memory creation/update timestamps

# Incomplete onboarding indicators
❌ Only 1-2 memories available
❌ Missing essential categories
❌ Only basic configuration documented
❌ No process or procedure documentation
```

## Integration with Development Workflow

### Project Startup Sequence
```
1. Activate project → Set project context
2. Check onboarding → Determine available knowledge
3. Perform onboarding (if needed) → Create essential memories
4. Begin development → With proper project knowledge
```

### Memory Usage Guidance
```
# When onboarding is complete
→ Reference memory list for available knowledge
→ Read specific memories as needed for tasks
→ Avoid reading all memories immediately
→ Use memory names to identify relevant content

# Memory reading strategy
→ Read setup memories for configuration tasks
→ Read process memories for development workflow
→ Read documentation memories for API/architecture work
→ Read troubleshooting memories when encountering issues
```

## Best Practices

### 1. Always Check Before Starting
```
✅ Check onboarding status before beginning any project work
✅ Call this check after activating project
✅ Use results to guide next steps
✅ Follow recommendations for onboarding

❌ Start work without checking onboarding
❌ Assume onboarding was performed
❌ Skip essential project knowledge gathering
❌ Proceed without understanding available resources
```

### 2. Understand Memory Purpose
```
✅ Use memory names to understand content
✅ Read memories only when relevant to current task
✅ Remember what memories are available
✅ Plan memory reading based on task requirements

❌ Read all memories immediately
❌ Ignore available memory information
❌ Repeatedly read the same memories
❌ Read memories without specific purpose
```

### 3. Follow Onboarding Recommendations
```
✅ Perform onboarding when recommended
✅ Complete missing documentation areas
✅ Create essential project memories
✅ Update outdated memories when found

❌ Skip onboarding when recommended
❌ Ignore missing documentation areas
❌ Work without essential project knowledge
❌ Leave outdated information uncorrected
```

## Common Onboarding Patterns

### New Project Setup
```
1. Check onboarding → Usually none performed
2. Perform onboarding → Create essential memories
3. Document setup → Technology stack, configuration
4. Document processes → Development, testing, deployment
```

### Existing Project
```
1. Check onboarding → May be complete or partial
2. Review available memories → Understand current knowledge
3. Identify gaps → Missing or outdated information
4. Complete documentation → Fill in missing areas
```

### Team Onboarding
```
1. Check onboarding → Usually complete for established projects
2. Review memory list → Understand available documentation
3. Read relevant memories → Based on role and tasks
4. Update memories → Add new knowledge and procedures
```

## Error Handling

### Memory System Issues
```
Error: "Cannot access memory system"
Solutions:
- Verify project is properly activated
- Check file system permissions
- Ensure memory system is properly configured
```

### Partial Memory Access
```
Warning: "Some memories may be inaccessible"
Solutions:
- Check individual memory permissions
- Verify memory file integrity
- Consider memory system maintenance
```

### Inconsistent Memory State
```
Warning: "Memory state appears inconsistent"
Solutions:
- Verify memory creation timestamps
- Check for corrupted memory files
- Consider memory system cleanup
```

## Memory List Interpretation

### Memory Name Patterns
```
# Configuration memories
project_setup, environment_config, build_config
→ Basic project configuration and setup information

# Process memories  
development_process, deployment_process, testing_strategy
→ Procedures and workflows for development activities

# Documentation memories
api_endpoints, architecture_overview, database_schema
→ Technical documentation and specifications

# Support memories
coding_standards, troubleshooting_guide, common_errors
→ Guidelines and problem-solving resources
```

### Memory Relevance Assessment
```
# Task-based memory relevance
Development task → Read: project_setup, coding_standards, development_process
API work → Read: api_endpoints, architecture_overview
Database work → Read: database_schema, environment_config
Deployment → Read: deployment_process, environment_config
Troubleshooting → Read: troubleshooting_guide, common_errors
```

This workflow replaces CheckOnboardingPerformedTool functionality for assessing project onboarding status and available documentation.