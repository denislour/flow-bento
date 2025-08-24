# Activate Project

## Function Description (Replaces ActivateProjectTool)

When user requests to activate a project by name or path, execute the following workflow to set up the project context and make it available for development operations:

## Step 1: Project Identification
**Description**: Identify the project to activate by name or path
**Requirements**:
- Project can be specified by registered name or directory path
- System should recognize existing projects vs new project creation
- Handle both absolute and relative paths appropriately

**Project Identification Examples**:
```
# By registered project name
Input: "my_web_app"
→ Activate existing registered project

# By directory path
Input: "/path/to/project"
→ Activate project at specific path

# By relative path
Input: "./frontend"
→ Activate project in current directory's frontend folder

# New project creation
Input: "/new/project/path"
→ Create and activate new project if path doesn't exist
```

## Step 2: Project Validation and Setup
**Description**: Validate project exists or create new project configuration
**Validation Process**:
- Check if project already exists in system
- Validate project directory structure
- Detect programming language and project type
- Create project configuration if needed

**Project Detection**:
```
# Existing project detection
Check: project name in registered projects
Check: project directory exists
Check: valid project structure

# New project creation
Action: create project configuration
Action: detect language from file extensions
Action: set up initial project metadata
```

## Step 3: Language and Configuration Detection
**Description**: Automatically detect project programming language and setup
**Language Detection Patterns**:
- Analyze file extensions and structure
- Check for configuration files (package.json, requirements.txt, etc.)
- Identify framework-specific patterns
- Set appropriate language server configuration

**Language Detection Examples**:
```
# Python project detection
Files: "*.py", "requirements.txt", "setup.py", "pyproject.toml"
→ Language: Python
→ Setup: Python language server

# JavaScript/Node.js project
Files: "package.json", "*.js", "*.ts", "node_modules/"
→ Language: JavaScript/TypeScript
→ Setup: TypeScript language server

# Java project
Files: "*.java", "pom.xml", "build.gradle", "src/main/java/"
→ Language: Java
→ Setup: Java language server

# Ruby project
Files: "*.rb", "Gemfile", "Rakefile", "app/", "config/"
→ Language: Ruby
→ Setup: Ruby language server
```

## Step 4: Project Context Activation
**Description**: Set up complete project context for development operations
**Activation Process**:
- Set project as active/current project
- Initialize language server if needed
- Load project-specific memories
- Configure available tools for project type
- Provide project information summary

**Context Setup**:
```
# Project state activation
→ Set as active project
→ Load project configuration
→ Initialize development environment
→ Enable project-specific tools

# Memory system activation
→ Load existing project memories
→ Make memories available for reference
→ Initialize memory system for project

# Tool activation
→ Enable file operations for project
→ Enable symbol analysis for detected language
→ Configure appropriate development tools
```

## Complete Workflow Examples

### Example 1: Activate Existing Project
**Request**: "Activate project my_web_app"

#### Step 1: Identify project
```
Input: "my_web_app"
Type: Registered project name
Action: Lookup existing project configuration
```

#### Step 2: Load configuration
```
Project: my_web_app
Path: /home/user/projects/my_web_app
Language: Python (FastAPI)
Status: Existing project
```

#### Step 3: Activate context
```
Action: Set as active project
Language server: Start Python language server
Memories: Load 5 existing memories
Tools: Enable Python development tools
```

#### Step 4: Expected output
```
"Activated existing project with name 'my_web_app' at /home/user/projects/my_web_app, language: Python

Additional project information:
FastAPI web application with PostgreSQL database. Uses Poetry for dependency management.

Available memories:
["project_setup", "api_endpoints", "database_schema", "deployment_process", "testing_strategy"]

Available tools:
["read_file", "create_file", "find_symbol", "replace_symbol", "execute_commands", "write_memory", "read_memory"]"
```

### Example 2: Create and Activate New Project
**Request**: "Activate project /home/user/new_project"

#### Step 1: Identify project
```
Input: "/home/user/new_project"
Type: Directory path
Status: New project (directory doesn't exist)
```

#### Step 2: Create project
```
Action: Create new project configuration
Path: /home/user/new_project
Language: Detected from files (or prompt user)
Configuration: Create initial project.yml
```

#### Step 3: Setup project context
```
Project name: Generated from directory name "new_project"
Language: Auto-detected or default
Initial memories: Empty
Tools: Enable based on language detection
```

#### Step 4: Expected output
```
"Created and activated a new project with name 'new_project' at /home/user/new_project, language: Python. You can activate this project later by name.

The project's configuration is in /home/user/new_project/.project/project.yml. In particular, you may want to edit the project name and the initial prompt.

Available memories:
[]
You should not read these memories directly, but rather use memory operations to access them later if needed for tasks.

Available tools:
["read_file", "create_file", "list_dir", "find_symbol", "execute_commands", "write_memory"]"
```

### Example 3: Activate Project with Existing Memories
**Request**: "Activate project backend_service"

#### Step 1: Load project
```
Project: backend_service
Path: /projects/backend_service
Language: Java (Spring Boot)
Status: Existing with rich context
```

#### Step 2: Load memories
```
Available memories: 8 memories found
- project_setup
- api_documentation
- database_schema
- security_guidelines
- deployment_procedures
- testing_framework
- performance_benchmarks
- troubleshooting_guide
```

#### Step 3: Expected output with memories
```
"Activated existing project with name 'backend_service' at /projects/backend_service, language: Java

Additional project information:
Spring Boot microservice with MySQL database and Redis caching. Uses Maven for build management and Docker for containerization.

Available memories:
["project_setup", "api_documentation", "database_schema", "security_guidelines", "deployment_procedures", "testing_framework", "performance_benchmarks", "troubleshooting_guide"]
You should not read these memories directly, but rather use memory operations to access them later if needed for tasks.

Available tools:
["read_file", "create_file", "find_symbol", "replace_symbol", "execute_commands", "write_memory", "read_memory", "list_memories"]"
```

## Project Configuration Structure

### Project Metadata
```yaml
# .project/project.yml
project_name: "my_web_app"
language: "python"
framework: "fastapi"
created_at: "2024-01-15"
last_activated: "2024-01-20"

initial_prompt: |
  This is a FastAPI web application with PostgreSQL database.
  Uses Poetry for dependency management and pytest for testing.
  
dependencies:
  - "postgresql"
  - "redis"
  - "poetry"

development:
  test_command: "poetry run pytest"
  start_command: "poetry run uvicorn main:app --reload"
  build_command: "poetry build"
```

### Language-Specific Configuration
```yaml
# Python project
language: "python"
language_server: "pyright"
file_patterns: ["*.py"]
test_patterns: ["test_*.py", "*_test.py"]

# JavaScript project
language: "javascript"
language_server: "typescript"
file_patterns: ["*.js", "*.ts", "*.jsx", "*.tsx"]
test_patterns: ["*.test.js", "*.spec.js"]

# Java project
language: "java"
language_server: "jdtls"
file_patterns: ["*.java"]
test_patterns: ["*Test.java"]
```

## Project Types and Detection

### Web Applications
```
# Python web apps
Indicators: "app.py", "main.py", "requirements.txt"
Frameworks: Flask, FastAPI, Django

# Node.js web apps  
Indicators: "package.json", "server.js", "app.js"
Frameworks: Express, Next.js, Nest.js

# Java web apps
Indicators: "pom.xml", "src/main/java", "@SpringBootApplication"
Frameworks: Spring Boot, Spring MVC
```

### Mobile Applications
```
# React Native
Indicators: "package.json", "metro.config.js", "App.js"
Platform: Cross-platform mobile

# Android
Indicators: "build.gradle", "AndroidManifest.xml"
Platform: Android native

# iOS
Indicators: "*.xcodeproj", "Info.plist", "*.swift"
Platform: iOS native
```

### Data Science Projects
```
# Python data science
Indicators: "*.ipynb", "requirements.txt", "data/"
Libraries: pandas, numpy, scikit-learn

# R projects
Indicators: "*.R", "*.Rmd", "DESCRIPTION"
Environment: R statistical computing
```

## Error Handling

### Project Not Found
```
Error: "Project 'nonexistent_project' not found in registered projects"
Solution: Check project name spelling or provide full path
```

### Invalid Path
```
Error: "Cannot access path '/invalid/path'"
Solution: Ensure path exists and is accessible
```

### Permission Denied
```
Error: "Permission denied accessing project directory"
Solution: Check directory permissions and access rights
```

### Language Detection Failed
```
Warning: "Could not detect project language, defaulting to Python"
Solution: Manually specify language or add language indicators
```

## Best Practices

### 1. Use Descriptive Project Names
```
✅ "ecommerce_api"        → Clear purpose
✅ "user_management_ui"   → Descriptive scope
✅ "analytics_dashboard"  → Obvious function

❌ "project1"            → Not descriptive
❌ "test"               → Too generic
❌ "my_app"             → Vague purpose
```

### 2. Organize Projects Logically
```
✅ Group related projects in directories
✅ Use consistent naming conventions
✅ Maintain clear project boundaries

❌ Mix different project types randomly
❌ Use inconsistent naming patterns
```

### 3. Maintain Project Configuration
```
✅ Keep project.yml updated
✅ Document project dependencies
✅ Include helpful initial prompts
✅ Set appropriate language configuration

❌ Leave configuration empty
❌ Use outdated information
❌ Ignore language detection issues
```

### 4. Use Memory System Effectively
```
✅ Create memories for project-specific information
✅ Document important procedures and configurations
✅ Keep memories updated and relevant

❌ Rely only on implicit knowledge
❌ Let memories become outdated
```

## Integration with Development Workflow

### After Project Activation
1. **Review project information**: Check language, framework, dependencies
2. **Load relevant memories**: Access project-specific knowledge
3. **Understand project structure**: Use file operations to explore
4. **Begin development tasks**: Use appropriate tools for project type

### Project Lifecycle Management
1. **Initial activation**: Create project, detect language, setup configuration
2. **Development**: Use project context for all operations
3. **Knowledge accumulation**: Store important information in memories
4. **Maintenance**: Update configuration and memories as project evolves

This workflow replaces ActivateProjectTool functionality for project context management and activation.