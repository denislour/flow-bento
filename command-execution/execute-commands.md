# Execute Commands

## Function Description (Replaces ExecuteShellCommandTool)

When user requests to execute shell commands in the project environment, execute the following workflow to run commands safely and capture output:

## Step 1: Command Specification and Validation
**Description**: Define the command to execute and validate safety
**Requirements**:
- Command must be safe (no destructive operations)
- Working directory should be specified or default to project root
- Consider command impact and security implications

**Command Safety Examples**:
```
# Safe commands
✅ "npm install"              → Install dependencies
✅ "python -m pytest"         → Run tests
✅ "git status"               → Check repository status
✅ "ls -la"                   → List directory contents
✅ "cat package.json"         → Read file content

# Unsafe commands
❌ "rm -rf /"                 → Destructive file deletion
❌ "sudo chmod 777 /"         → Dangerous permission changes
❌ "curl malicious-url"       → Potential security risk
❌ "dd if=/dev/zero"          → System destructive operation
```

## Step 2: Environment Setup
**Description**: Configure execution environment and working directory
**Environment Configuration**:
- Set working directory (default: project root)
- Configure environment variables if needed
- Ensure proper permissions and access

**Working Directory Examples**:
```
# Default to project root
Command: "npm install"
CWD: /project/root/

# Specific subdirectory
Command: "python setup.py test"
CWD: /project/root/backend/

# Script directory
Command: "./deploy.sh"
CWD: /project/root/scripts/
```

## Step 3: Execute Command with Output Capture
**Description**: Run the command and capture stdout/stderr
**Execution Options**:
- Capture standard output (stdout)
- Capture error output (stderr) - optional
- Set timeout limits to prevent hanging
- Handle command completion and exit codes

**Output Capture Configuration**:
```
# Standard output only
→ Capture: stdout
→ Stderr: ignore

# Both stdout and stderr
→ Capture: stdout + stderr
→ Combined: for complete output

# Error handling
→ Exit code: 0 (success) vs non-zero (error)
→ Timeout: prevent infinite execution
```

## Step 4: Format and Return Results
**Description**: Process command output and provide structured results
**Result Format**:
- JSON structure with stdout, stderr, and metadata
- Include execution status and exit codes
- Handle output length limits
- Provide execution timing information

**Standard Output Format**:
```json
{
  "stdout": "Command output text",
  "stderr": "Error output text",
  "exit_code": 0,
  "execution_time": "2.5s",
  "working_directory": "/project/root"
}
```

## Complete Workflow Examples

### Example 1: Install Dependencies
**Request**: "Execute npm install to install project dependencies"

#### Step 1: Validate command
```
Command: "npm install"
Safety: ✅ Safe dependency installation
Purpose: Install Node.js dependencies
```

#### Step 2: Setup environment
```
Working directory: project root
Environment: inherit system environment
Timeout: 300 seconds (5 minutes)
```

#### Step 3: Execute and capture
```
Execute: npm install
Capture: stdout and stderr
Monitor: progress and completion
```

#### Step 4: Expected output
```json
{
  "stdout": "npm WARN deprecated package@1.0.0: Package deprecated\nnpm WARN optional SKIPPING OPTIONAL DEPENDENCY\nadded 150 packages from 200 contributors in 45.234s",
  "stderr": "",
  "exit_code": 0,
  "execution_time": "45.2s",
  "working_directory": "/project/root"
}
```

### Example 2: Run Tests
**Request**: "Execute python -m pytest to run test suite"

#### Step 1: Validate command
```
Command: "python -m pytest"
Safety: ✅ Safe test execution
Purpose: Run Python test suite
```

#### Step 2: Setup environment
```
Working directory: project root
Environment: include test environment variables
Capture stderr: yes (for test failures)
```

#### Step 3: Execute and capture
```
Execute: python -m pytest
Capture: both stdout and stderr
Include: test results and any errors
```

#### Step 4: Expected output
```json
{
  "stdout": "========================= test session starts =========================\ncollected 25 items\n\ntests/test_user.py .....                                    [ 20%]\ntests/test_auth.py .....                                    [ 40%]\ntests/test_api.py .....                                     [ 60%]\ntests/test_models.py .....                                  [ 80%]\ntests/test_utils.py .....                                   [100%]\n\n========================= 25 passed in 3.45s =========================",
  "stderr": "",
  "exit_code": 0,
  "execution_time": "3.5s",
  "working_directory": "/project/root"
}
```

### Example 3: Check Git Status
**Request**: "Execute git status to check repository state"

#### Step 1: Validate command
```
Command: "git status"
Safety: ✅ Safe read-only operation
Purpose: Check repository status
```

#### Step 2: Setup and execute
```
Working directory: project root
Execute: git status --porcelain (for cleaner output)
```

#### Step 3: Expected output
```json
{
  "stdout": " M src/models/user.py\n A src/services/email.py\n?? docs/new_feature.md",
  "stderr": "",
  "exit_code": 0,
  "execution_time": "0.2s",
  "working_directory": "/project/root"
}
```

## Common Command Categories

### Development Commands
```bash
# Package management
"npm install"           → Install Node.js dependencies
"pip install -r requirements.txt" → Install Python dependencies
"composer install"      → Install PHP dependencies

# Build commands
"npm run build"         → Build frontend assets
"python setup.py build" → Build Python package
"make build"           → Run Makefile build target

# Test commands
"npm test"             → Run JavaScript tests
"python -m pytest"    → Run Python tests
"mvn test"            → Run Java tests with Maven
```

### Repository Commands
```bash
# Git operations
"git status"           → Check repository status
"git log --oneline -10" → Show recent commits
"git diff"             → Show working directory changes
"git branch"           → List branches

# Repository information
"git remote -v"        → Show remote repositories
"git config --list"    → Show git configuration
```

### System Information
```bash
# Environment info
"node --version"       → Check Node.js version
"python --version"     → Check Python version
"java -version"        → Check Java version

# System info
"ls -la"              → List directory contents
"pwd"                 → Show current directory
"whoami"              → Show current user
```

### Project-Specific Scripts
```bash
# Custom scripts
"./scripts/deploy.sh"  → Run deployment script
"./scripts/backup.sh"  → Run backup script
"python manage.py migrate" → Run Django migrations
```

## Safety Guidelines

### Safe Command Types
```
✅ Read-only operations (ls, cat, git status)
✅ Build and test commands (npm test, pytest)
✅ Package installation (npm install, pip install)
✅ Development tools (linting, formatting)
✅ Project-specific scripts (documented and reviewed)
```

### Commands to Avoid
```
❌ File deletion (rm, del)
❌ Permission changes (chmod, chown)
❌ System modifications (sudo commands)
❌ Network downloads from untrusted sources
❌ Process killers (kill, killall)
❌ Disk operations (dd, fdisk)
```

### Pre-execution Validation
```python
# Command validation checklist
def validate_command(command):
    dangerous_patterns = [
        "rm -rf",
        "sudo",
        "chmod 777",
        "dd if=",
        "wget http://",
        "curl http://"
    ]
    
    for pattern in dangerous_patterns:
        if pattern in command:
            return False, f"Dangerous pattern detected: {pattern}"
    
    return True, "Command appears safe"
```

## Error Handling

### Command Not Found
```json
{
  "stdout": "",
  "stderr": "command not found: nonexistent-command",
  "exit_code": 127,
  "error": "Command not found"
}
```

### Permission Denied
```json
{
  "stdout": "",
  "stderr": "permission denied: ./script.sh",
  "exit_code": 126,
  "error": "Permission denied"
}
```

### Command Timeout
```json
{
  "stdout": "partial output...",
  "stderr": "",
  "exit_code": -1,
  "error": "Command timed out after 300 seconds"
}
```

### Non-zero Exit Code
```json
{
  "stdout": "some output",
  "stderr": "error: test failed",
  "exit_code": 1,
  "error": "Command failed with exit code 1"
}
```

## Best Practices

### 1. Check Existing Memory
Always check if there's memory about suggested commands before executing:
```
✅ Read memory "deployment_commands" first
✅ Follow documented procedures
✅ Use known-safe command patterns
```

### 2. Use Appropriate Working Directory
```
✅ Specify correct working directory for command context
✅ Use project root for general commands
✅ Use subdirectories for specific operations
```

### 3. Handle Output Appropriately
```
✅ Capture both stdout and stderr for debugging
✅ Respect output length limits
✅ Parse structured output when possible
```

### 4. Security Considerations
```
✅ Validate command safety before execution
✅ Avoid commands that modify system state
✅ Use read-only operations when possible
✅ Never execute untrusted user input directly
```

## Integration with Development Workflow

### Before Command Execution
1. **Check memory**: Look for documented procedures
2. **Validate safety**: Ensure command is safe to run
3. **Set context**: Configure proper working directory
4. **Plan output**: Decide what output to capture

### After Command Execution
1. **Check results**: Verify command succeeded
2. **Handle errors**: Deal with failures appropriately
3. **Parse output**: Extract useful information
4. **Document**: Save useful patterns to memory

### Common Workflows
```
# Test workflow
1. Execute: "python -m pytest"
2. Parse: test results and failures
3. Report: success/failure status

# Build workflow
1. Execute: "npm run build"
2. Monitor: build progress
3. Verify: build artifacts created

# Deployment workflow
1. Execute: "./scripts/deploy.sh"
2. Monitor: deployment progress
3. Verify: deployment success
```

This workflow replaces ExecuteShellCommandTool functionality for safe command execution with proper output capture and error handling.