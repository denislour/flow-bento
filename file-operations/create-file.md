# Create File

## Function Description (Replaces CreateTextFileTool)

When user requests to create/overwrite a file in the project directory, execute the following workflow to write new files or overwrite existing files with UTF-8 encoding:

## Step 1: Specify File Path and Content
**Description**: Define the target file location and content to write
**Requirements**:
- File path must be within project directory
- Use relative path from project root
- Provide complete file content
- Handle UTF-8 encoding properly

**File Creation Examples**:
```
# New source file
Target: "src/models/product.py"
Content: Python class implementation

# Configuration file
Target: "config/database.yml"
Content: YAML configuration

# Documentation file
Target: "docs/api.md"
Content: Markdown documentation

# Script file
Target: "scripts/deploy.sh"
Content: Shell script
```

## Step 2: Validate Path and Permissions
**Description**: Ensure file can be created at specified location
**Validation Requirements**:
- Path must be within project boundaries
- Parent directories will be created if needed
- Check for overwrite scenarios
- Validate write permissions

**Path Validation**:
```
# Valid paths (within project)
✅ "src/new_module.py"        → /project/src/new_module.py
✅ "docs/guide.md"           → /project/docs/guide.md
✅ "config/settings.json"    → /project/config/settings.json

# Invalid paths
❌ "/absolute/path/file.py"  → Error: outside project
❌ "../outside/file.py"      → Error: outside project
❌ "~/user/file.py"         → Error: absolute path
```

## Step 3: Create Directory Structure
**Description**: Ensure parent directories exist before file creation
**Directory Creation**:
- Create parent directories automatically if they don't exist
- Maintain proper directory permissions
- Handle nested directory structures

**Directory Creation Examples**:
```
# Single level directory
"src/new_file.py" → Create "src/" if needed

# Nested directories
"docs/api/endpoints.md" → Create "docs/" and "docs/api/" if needed

# Deep nesting
"src/components/ui/button.tsx" → Create entire path if needed
```

## Step 4: Write File Content
**Description**: Write content to file with proper encoding and formatting
**Writing Process**:
- Use UTF-8 encoding for all text files
- Preserve line endings and formatting
- Handle file overwriting safely
- Provide creation confirmation

**Content Handling**:
```
# Text content with proper encoding
→ Write UTF-8 encoded content
→ Preserve line breaks and indentation
→ Handle special characters properly

# Overwrite handling
→ Detect existing files
→ Safely overwrite if specified
→ Provide overwrite confirmation
```

## Complete Workflow Examples

### Example 1: Create New Python Module
**Request**: "Create file src/services/email.py with email service implementation"

#### Step 1: Specify parameters
```
File: "src/services/email.py"
Content: Python class for email service
Encoding: UTF-8
```

#### Step 2: Validate path
```
Check: path within project boundaries
Check: "src/services/" directory exists or can be created
Action: proceed with creation
```

#### Step 3: Create directories
```
Check: "src/" exists ✓
Check: "src/services/" exists → Create if needed
Result: directory structure ready
```

#### Step 4: Write content
```python
# Content to write:
import smtplib
from email.mime.text import MIMEText
from email.mime.multipart import MIMEMultipart

class EmailService:
    def __init__(self, smtp_server, port, username, password):
        self.smtp_server = smtp_server
        self.port = port
        self.username = username
        self.password = password
    
    def send_email(self, to_email, subject, body):
        """Send email to specified recipient."""
        msg = MIMEMultipart()
        msg['From'] = self.username
        msg['To'] = to_email
        msg['Subject'] = subject
        
        msg.attach(MIMEText(body, 'plain'))
        
        try:
            server = smtplib.SMTP(self.smtp_server, self.port)
            server.starttls()
            server.login(self.username, self.password)
            text = msg.as_string()
            server.sendmail(self.username, to_email, text)
            server.quit()
            return True
        except Exception as e:
            print(f"Error sending email: {e}")
            return False
```

#### Expected output
```
"File created: src/services/email.py."
```

### Example 2: Create Configuration File
**Request**: "Create file config/database.yml with database configuration"

#### Step 1: Specify parameters
```
File: "config/database.yml"
Content: YAML database configuration
```

#### Step 2: Write content
```yaml
# Content to write:
development:
  adapter: postgresql
  database: myapp_development
  username: postgres
  password: password
  host: localhost
  port: 5432

test:
  adapter: postgresql
  database: myapp_test
  username: postgres
  password: password
  host: localhost
  port: 5432

production:
  adapter: postgresql
  database: myapp_production
  username: <%= ENV['DATABASE_USERNAME'] %>
  password: <%= ENV['DATABASE_PASSWORD'] %>
  host: <%= ENV['DATABASE_HOST'] %>
  port: <%= ENV['DATABASE_PORT'] %>
```

### Example 3: Overwrite Existing File
**Request**: "Create file README.md with updated project documentation"

#### Step 1: Detect existing file
```
File: "README.md"
Status: already exists
Action: will overwrite existing file
```

#### Step 2: Write new content
```markdown
# Project Name

## Description
This project provides a comprehensive solution for...

## Installation
```bash
npm install
# or
pip install -r requirements.txt
```

## Usage
```python
from myproject import MyClass

instance = MyClass()
result = instance.process()
```

## Contributing
Please read CONTRIBUTING.md for details on our code of conduct.

## License
This project is licensed under the MIT License.
```

#### Expected output
```
"File created: README.md. Overwrote existing file."
```

## File Type Handling

### Source Code Files
```python
# Python files
"src/models/user.py" → Python class/module

# JavaScript files
"src/components/App.js" → React component

# Java files
"src/main/java/User.java" → Java class

# Ruby files
"app/models/user.rb" → Ruby class
```

### Configuration Files
```yaml
# YAML configuration
"config/application.yml" → YAML config

# JSON configuration
"package.json" → NPM package config

# INI files
"config.ini" → INI format config

# Environment files
".env.example" → Environment variables
```

### Documentation Files
```markdown
# Markdown documentation
"docs/README.md" → Project documentation

# Text files
"LICENSE.txt" → License text

# API documentation
"docs/api/endpoints.md" → API docs
```

### Script Files
```bash
# Shell scripts
"scripts/deploy.sh" → Deployment script

# Python scripts
"scripts/setup.py" → Setup script

# Batch files
"scripts/build.bat" → Windows batch script
```

## Common Use Cases

### 1. Create New Module
**Request**: Create new Python/Ruby/Java module
- Define class structure
- Add initial implementation
- Set up proper imports

### 2. Add Configuration
**Request**: Create configuration files
- Database configuration
- Application settings
- Environment variables

### 3. Documentation Creation
**Request**: Create documentation files
- README files
- API documentation
- User instruction

### 4. Script Creation
**Request**: Create utility scripts
- Build scripts
- Deployment scripts
- Data processing scripts

## Best Practices

### 1. Use Descriptive Paths
```
✅ "src/services/payment_processor.py"
✅ "docs/user_instructions.md"
✅ "config/database_settings.yml"

❌ "file.py"
❌ "temp.txt"
❌ "new_document.md"
```

### 2. Organize by Purpose
```
✅ Group related files in appropriate directories
✅ Follow project structure conventions
✅ Use consistent naming patterns

❌ Put all files in root directory
❌ Mix different file types randomly
```

### 3. Include Proper Headers
```python
# Python files - include imports and docstrings
"""Module for handling user authentication."""

import bcrypt
from datetime import datetime

class AuthService:
    """Service for user authentication operations."""
    pass
```

### 4. Handle Encoding Properly
```
✅ Always use UTF-8 encoding
✅ Handle special characters properly
✅ Preserve line endings

❌ Use system default encoding
❌ Ignore character encoding issues
```

## Error Handling

### Path Outside Project
```
Error: "Cannot create file outside of the project directory"
Solution: Use relative path within project
```

### Permission Denied
```
Error: "Permission denied writing to file"
Solution: Check directory permissions and write access
```

### Invalid File Name
```
Error: "Invalid file name or path"
Solution: Use valid file names without special characters
```

### Directory Creation Failed
```
Error: "Cannot create parent directories"
Solution: Check parent directory permissions
```

## Advanced Usage

### Content Templates
```python
# Python class template
class_template = '''
class {class_name}:
    """Class for {description}."""
    
    def __init__(self):
        pass
    
    def process(self):
        """Main processing method."""
        pass
'''

# Configuration template
config_template = '''
# Configuration for {project_name}
database:
  host: localhost
  port: 5432
  name: {db_name}
'''
```

### File Generation Patterns
```
# Model files
"src/models/{entity_name}.py"

# Test files
"tests/test_{module_name}.py"

# Documentation files
"docs/{feature_name}.md"
```

## Integration with Development Workflow

### After File Creation
1. **Validate syntax**: Check created file for syntax errors
2. **Add to version control**: Include in git if appropriate
3. **Update documentation**: Reference new file in docs
4. **Run tests**: Ensure new file doesn't break existing code

### File Creation Patterns
1. **Create**: Write new file content
2. **Validate**: Check file syntax and structure
3. **Integrate**: Ensure compatibility with existing code
4. **Document**: Update relevant documentation

This workflow replaces CreateTextFileTool functionality for creating new files and overwriting existing ones with proper encoding and error handling.