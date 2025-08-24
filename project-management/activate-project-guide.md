# Activate Project Guide

## Overview
The `activate_project` tool activates a project by name or path, setting it as the active context for all subsequent operations. This is typically the first step when starting work on any project.

## Request Template

```
"Activate project [PROJECT_IDENTIFIER] and show [INFORMATION_LEVEL]"
```

## Required Parameters

### **PROJECT_IDENTIFIER** (Mandatory)
How to identify the project to activate:

#### By Name (Registered Projects)
- `"my-web-app"` - Previously registered project name
- `"flow-bento-tools"` - Another registered project
- `"backend-api"` - Named project

#### By Path (New or Existing Projects)
- `"/absolute/path/to/project"` - Full absolute path
- `"../relative/path/to/project"` - Relative path
- `"."` - Current directory
- `"~/projects/my-app"` - Home directory relative path

## Optional Parameters

### **INFORMATION_LEVEL**
What information to display after activation:
- `"basic info"` - Just confirmation of activation (default)
- `"project details"` - Include project configuration and language
- `"full overview"` - All project info, memories, and available tools
- `"memories list"` - Show available project memories
- `"tools list"` - Show available tools for this project

## Example Requests

### 1. Activate by Name (Existing Project)
**Request**: "Activate project flow-bento-tools and show full overview"

**Tool Parameters**:
```python
project="flow-bento-tools"
```

**Expected Output**:
```
Activated existing project with name 'flow-bento-tools' at /path/to/flow-bento-tools, language: python

Additional project information:
Advanced MCP server for code analysis and modification with 35+ tools organized in 7 categories.

Available memories:
["project_structure", "tool_overview", "development_setup", "common_patterns"]
You should not read these memories directly, but rather use the `read_memory` tool to read them later if needed for the task.

Available tools:
["read_file", "find_symbol", "find_referencing_symbols", "activate_project", "write_memory", "execute_shell_command", ...]
```

### 2. Activate by Path (New Project)
**Request**: "Activate project /home/user/new-project and show project details"

**Tool Parameters**:
```python
project="/home/user/new-project"
```

**Expected Output**:
```
Created and activated a new project with name 'new-project' at /home/user/new-project, language: python. 
You can activate this project later by name.

The project's Flow-Bento configuration is in /home/user/new-project/.flow-bento/project.yml. In particular, you may want to edit the project name and the initial prompt.

Available memories:
[]

Available tools:
["read_file", "create_text_file", "list_dir", "find_file", "activate_project", ...]
```

### 3. Quick Activation
**Request**: "Activate project . and show basic info"

**Tool Parameters**:
```python
project="."
```

**Expected Output**:
```
Activated existing project with name 'current-directory' at /current/working/directory, language: python
```

## Project Configuration

### Automatic Language Detection
When activating a new project, Flow-Bento automatically detects the programming language based on:
- File extensions in the project
- Configuration files (package.json, setup.py, pom.xml, etc.)
- Directory structure patterns

### Project Registration
- **New projects** are automatically registered when first activated by path
- **Registered projects** can be activated by name in future sessions
- Project names are derived from directory names unless specified

### Configuration File Creation
For new projects, Flow-Bento creates `.flow-bento/project.yml` containing:
```yaml
name: "project-name"
language: "python"
initial_prompt: "Project description and setup instructions"
ignored_paths:
  - ".git/"
  - "node_modules/"
  - "__pycache__/"
```

## Understanding the Output

### Project Status Indicators
- **"Activated existing project"** - Project was previously registered
- **"Created and activated"** - New project, now registered
- **"You can activate this project later by name"** - Project is now registered

### Language Information
- **language: python** - Detected programming language
- Affects available tools and analysis capabilities
- Influences syntax highlighting and parsing

### Available Memories
- **Empty list []** - New project with no stored information
- **Named memories** - Previously stored project-specific information
- Use `read_memory` tool to access specific memories when needed

### Available Tools
- **Core tools** - Always available (file operations, project management)
- **Language-specific tools** - Based on detected project language
- **Optional tools** - May be enabled/disabled based on configuration

## Common Use Cases

### 1. Start Working on Existing Project
**Request**: "Activate project my-web-app and show full overview"
- Sets context for all future operations
- Shows what information is available
- Lists available tools for the project

### 2. Initialize New Project
**Request**: "Activate project /path/to/new-project and show project details"
- Creates new project configuration
- Registers project for future use
- Sets up initial context

### 3. Switch Between Projects
**Request**: "Activate project backend-api and show basic info"
- Quickly switch context
- Minimal output for efficient workflow
- Ready for immediate work

### 4. Project Discovery
**Request**: "Activate project . and show memories list"
- Discover what's known about current directory
- See available project memories
- Understand project context

## Project State After Activation

Once a project is activated, it becomes the active context for:

### File Operations
- All relative paths resolve to project root
- File listings respect project ignore patterns
- Search operations scope to project boundaries

### Symbol Analysis
- Language server starts for the project language
- Symbol searches scope to project files
- Code analysis uses project-specific settings

### Memory Operations
- Memory storage/retrieval uses project-specific location
- Memories are isolated per project
- Cross-project memories are not accessible

### Command Execution
- Shell commands execute from project root
- Environment variables respect project settings
- Build commands use project-specific tools

## Error Handling

### Invalid Project Path
```
Request: "Activate project /nonexistent/path"
Error: "Project path does not exist or is not accessible"
Solution: Verify the path exists and you have access permissions
```

### Permission Issues
```
Request: "Activate project /restricted/path"
Error: "Permission denied accessing project directory"
Solution: Check file system permissions or use a different path
```

### Configuration Conflicts
```
Request: "Activate project conflicted-name"
Error: "Multiple projects found with same name"
Solution: Use full path instead of name, or rename one project
```

## Best Practices

### 1. Always Activate Before Starting
```
✅ First: "Activate project my-app"
✅ Then: "Find class User in this project"

❌ Wrong: "Find class User" (without active project)
```

### 2. Use Descriptive Project Names
```
✅ "web-frontend"
✅ "api-backend"
✅ "ml-training"

❌ "project1"
❌ "test"
❌ "temp"
```

### 3. Check Available Resources
```
✅ "Activate project name and show full overview"
- See what memories and tools are available
- Understand project context before proceeding
```

### 4. Maintain Clean Project Structure
- Keep `.flow-bento/` directory in version control
- Document project-specific setup in initial_prompt
- Use meaningful memory names for stored information

## Integration with Other Tools

### After Project Activation
1. **Check onboarding**: Use `check_onboarding_performed` tool
2. **Read memories**: Use `read_memory` for relevant project information
3. **Explore structure**: Use `list_dir` and `get_symbols_overview`
4. **Begin analysis**: Use symbol analysis tools as needed

### Project Configuration Management
- **Switch modes**: Change operation modes for different workflows
- **Update settings**: Modify `.flow-bento/project.yml` as needed
- **Memory management**: Store and organize project-specific information

This guide enables you to properly initialize and switch between project contexts, ensuring all subsequent operations work within the correct project scope.