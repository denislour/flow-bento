# Onboarding

## Function Description (Replaces OnboardingTool)

When project onboarding has not been performed yet, execute the following workflow to gather essential project information and create comprehensive documentation memories:

## Step 1: Determine System Environment
**Description**: Identify the operating system and development environment
**Environment Detection**:
- Detect operating system (Windows, macOS, Linux)
- Identify development tools and IDEs available
- Determine system-specific configuration requirements
- Assess platform-specific development practices

**System-Specific Considerations**:
```
# Windows Environment
→ PowerShell/Command Prompt usage
→ Windows-specific path handling
→ Visual Studio/VS Code integration
→ Windows package managers (Chocolatey, winget)

# macOS Environment  
→ Terminal and shell configuration
→ Homebrew package management
→ Xcode development tools
→ macOS-specific file system considerations

# Linux Environment
→ Distribution-specific package managers
→ Shell environment configuration
→ Development tool availability
→ Container/virtualization setup
```

## Step 2: Analyze Project Structure
**Description**: Examine the codebase to understand project organization and technology stack
**Structure Analysis Process**:
- Scan root directory for configuration files
- Identify primary programming languages
- Detect frameworks and libraries used
- Understand build system and dependency management
- Map directory structure and organization

**Technology Stack Detection**:
```
# Configuration Files Analysis
package.json        → Node.js/JavaScript project
requirements.txt    → Python project with pip
Pipfile            → Python project with pipenv
pom.xml            → Java project with Maven
build.gradle       → Java/Kotlin project with Gradle
Cargo.toml         → Rust project
composer.json      → PHP project
Gemfile           → Ruby project

# Framework Detection
package.json (React/Vue/Angular) → Frontend framework
manage.py         → Django Python project  
app.py           → Flask Python project
pom.xml (Spring) → Spring Boot Java project
```

## Step 3: Create Essential Project Memories
**Description**: Document critical project information in memory storage
**Essential Memories to Create**:
- **project_setup**: Technology stack and configuration
- **development_process**: Build, test, and development workflow
- **environment_config**: Environment variables and setup
- **coding_standards**: Code style and conventions

**Memory Creation Process**:
```
# Technology Stack Documentation
→ Programming languages and versions
→ Frameworks and libraries used
→ Build tools and dependency managers
→ Development environment requirements

# Development Workflow Documentation
→ How to install dependencies
→ How to run the application
→ How to run tests
→ How to build for production

# Environment Configuration
→ Required environment variables
→ Database configuration
→ API keys and secrets management
→ Development vs production settings
```

## Step 4: Document Build and Test Procedures
**Description**: Create memories for essential development operations
**Procedure Documentation**:
- Document dependency installation process
- Record application startup procedures
- Document testing strategies and commands
- Record build and deployment processes

**Common Development Commands**:
```
# Node.js Projects
npm install          → Install dependencies
npm start           → Start development server
npm test            → Run test suite
npm run build       → Build for production

# Python Projects  
pip install -r requirements.txt → Install dependencies
python manage.py runserver      → Start Django server
python -m pytest              → Run tests
python setup.py build         → Build package

# Java Projects
mvn install         → Install dependencies with Maven
mvn spring-boot:run → Start Spring Boot application
mvn test           → Run tests
mvn package        → Build package
```

## Complete Workflow Examples

### Example 1: Node.js React Project Onboarding
**Request**: "Perform onboarding for this project"

#### Step 1: Detect environment
```
System: Windows 11
Development tools: VS Code, Node.js 18.x
Package manager: npm
Shell: PowerShell
```

#### Step 2: Analyze project
```
Root files found:
- package.json (React application)
- package-lock.json (npm lockfile)
- public/ directory (static assets)
- src/ directory (source code)
- .env.example (environment template)

Technology stack detected:
- React 18.x frontend framework
- TypeScript for type safety
- Express.js backend API
- PostgreSQL database
- Jest testing framework
```

#### Step 3: Create project_setup memory
```markdown
# Project Setup Information

## Technology Stack
- **Frontend**: React 18.x with TypeScript
- **Backend**: Express.js with Node.js 18.x
- **Database**: PostgreSQL 13+
- **Testing**: Jest with React Testing Library
- **Build Tool**: Create React App (CRA)
- **Package Manager**: npm

## Development Environment
- **Node.js**: 18.x or higher
- **npm**: 8.x or higher
- **PostgreSQL**: 13+ for local development
- **Git**: Version control

## Key Dependencies
```json
{
  "react": "^18.2.0",
  "typescript": "^4.9.0",
  "express": "^4.18.0",
  "pg": "^8.8.0",
  "jest": "^29.0.0"
}
```

## Environment Variables
- `DATABASE_URL`: PostgreSQL connection string
- `API_BASE_URL`: Backend API base URL
- `JWT_SECRET`: JWT signing secret
```

#### Step 4: Create development_process memory
```markdown
# Development Process

## Getting Started
1. Clone the repository
2. Install dependencies: `npm install`
3. Copy `.env.example` to `.env` and configure
4. Start PostgreSQL database
5. Run migrations: `npm run migrate`
6. Start development server: `npm start`

## Development Commands
- `npm install` - Install dependencies
- `npm start` - Start development server (port 3000)
- `npm test` - Run test suite
- `npm run build` - Build for production
- `npm run migrate` - Run database migrations

## Testing Strategy
- Unit tests with Jest
- Component tests with React Testing Library
- Integration tests for API endpoints
- Run tests before committing: `npm test`

## Build Process
- Production build: `npm run build`
- Outputs to `build/` directory
- Static files ready for deployment
```

### Example 2: Python Django Project Onboarding
**Request**: "Perform project onboarding"

#### Step 1: Detect environment
```
System: Ubuntu 22.04 LTS
Python: 3.10
Package manager: pip with virtualenv
Shell: bash
```

#### Step 2: Analyze project
```
Root files found:
- manage.py (Django project)
- requirements.txt (Python dependencies)
- .env.example (environment template)
- apps/ directory (Django applications)
- config/ directory (Django settings)

Technology stack detected:
- Django 4.2 web framework
- PostgreSQL database with psycopg2
- Redis for caching
- Celery for background tasks
- pytest for testing
```

#### Step 3: Create comprehensive memories
```markdown
# Project Setup Information

## Technology Stack
- **Framework**: Django 4.2
- **Python**: 3.10+
- **Database**: PostgreSQL 13+
- **Cache**: Redis 6+
- **Task Queue**: Celery with Redis broker
- **Testing**: pytest with Django extensions

## System Requirements
- Python 3.10 or higher
- PostgreSQL 13+
- Redis 6+
- Virtual environment (venv or virtualenv)

## Installation Process
1. Create virtual environment: `python -m venv venv`
2. Activate environment: `source venv/bin/activate`
3. Install dependencies: `pip install -r requirements.txt`
4. Configure environment variables
5. Run migrations: `python manage.py migrate`
6. Create superuser: `python manage.py createsuperuser`
```

### Example 3: Java Spring Boot Project Onboarding
**Request**: "Perform onboarding for this Java project"

#### Step 1: Detect environment
```
System: macOS
Java: OpenJDK 17
Build tool: Maven 3.8
IDE: IntelliJ IDEA
```

#### Step 2: Analyze project
```
Root files found:
- pom.xml (Maven configuration)
- src/main/java/ (Java source code)
- src/main/resources/ (Resources and configuration)
- application.yml (Spring Boot configuration)

Technology stack detected:
- Spring Boot 3.1
- Spring Data JPA
- MySQL database
- Maven build system
- JUnit 5 for testing
```

## Onboarding Instructions Template

### System-Specific Onboarding Guidance
```
# Windows Development Environment
→ Use PowerShell or Command Prompt for command execution
→ Configure Windows Defender exclusions for development directories
→ Install Windows Subsystem for Linux (WSL) if needed
→ Use Windows package managers: chocolatey, winget, or scoop

# macOS Development Environment  
→ Install Xcode Command Line Tools: xcode-select --install
→ Use Homebrew for package management: /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
→ Configure shell environment (zsh by default)
→ Set up development tools via Homebrew

# Linux Development Environment
→ Update package lists: sudo apt update (Ubuntu/Debian)
→ Install build essentials: sudo apt install build-essential
→ Configure development environment based on distribution
→ Use distribution package manager for tool installation
```

### Memory Creation Strategy
```
# Essential Memories (Always Create)
1. project_setup - Technology stack and configuration
2. development_process - Development workflow and commands
3. environment_config - Environment variables and setup
4. testing_strategy - Testing approach and commands

# Additional Memories (Based on Project)
5. deployment_process - If deployment info available
6. database_schema - If database documentation exists
7. api_endpoints - If API documentation available
8. coding_standards - If style guides exist
```

## Best Practices

### 1. Comprehensive Analysis
```
✅ Examine all configuration files thoroughly
✅ Identify all major technologies and frameworks
✅ Document version requirements clearly
✅ Include system-specific considerations

❌ Skip important configuration files
❌ Miss secondary technologies or tools
❌ Ignore version requirements
❌ Assume universal development practices
```

### 2. Practical Documentation
```
✅ Include working commands and procedures
✅ Provide step-by-step setup instructions
✅ Document common development tasks
✅ Include troubleshooting information

❌ Create theoretical documentation only
❌ Skip essential setup steps
❌ Ignore common development workflows
❌ Omit error handling and troubleshooting
```

### 3. Environment Awareness
```
✅ Tailor instructions to detected operating system
✅ Include platform-specific tools and commands
✅ Consider different development environments
✅ Provide alternatives for different setups

❌ Assume single development environment
❌ Ignore platform differences
❌ Use only one set of tools/commands
❌ Skip environment-specific configuration
```

## Integration with Development Workflow

### After Onboarding Completion
```
1. Onboarding creates essential memories
2. Check onboarding status shows completion
3. Available memories can be read as needed
4. Development work can begin with proper context
```

### Memory Usage After Onboarding
```
→ Read project_setup for technology stack questions
→ Read development_process for build/test procedures
→ Read environment_config for setup issues
→ Read testing_strategy for testing approach
```

### Continuous Improvement
```
→ Update memories as project evolves
→ Add new memories for discovered procedures
→ Refine documentation based on team feedback
→ Keep onboarding information current
```

This workflow replaces OnboardingTool functionality for comprehensive project analysis and documentation creation.