# Replace Symbol Body

## Function Description (Replaces ReplaceSymbolBodyTool)

When user requests to replace/modify implementation content of a symbol (class, method, function) in **ANY programming language** (Python, Ruby, Java, JavaScript, C#, Go, etc.), execute the following workflow using natural language:

## Step 1: Locate Symbol to Replace
**Description**: Use code search functionality to precisely locate the symbol to replace
**Search Requirements**:
- Search by specific symbol name
- Apply symbol type filters (class, method, function)
- Focus on appropriate search scope

**Language-Specific Examples**:
```
# Python
User: "Replace method login in class User"
→ Search: "def login" within User class scope, filter method type

# Ruby
User: "Replace method authenticate in UserService"
→ Search: "def authenticate" within UserService scope, filter method type

# Java
User: "Replace method processPayment in PaymentService"
→ Search: "processPayment" within PaymentService scope, filter method type

# JavaScript/TypeScript
User: "Replace function handleLogin"
→ Search: "handleLogin" in entire project, filter function type
```

## Step 2: Read Current Implementation
**Description**: Access and read current implementation content of the symbol
**Reading Requirements**:
- Read complete symbol content from start line to end line
- Include dependencies to understand context
- Record exact indentation and existing structure

**Language-Specific Examples**:
```
# Python
→ Read file "src/models/user.py" from line 25 to line 40, include dependencies

# Ruby
→ Read file "app/models/user.rb" from line 15 to line 30, include dependencies

# Java
→ Read file "src/main/java/com/example/User.java" from line 45 to line 65, include dependencies

# JavaScript
→ Read file "src/services/userService.js" from line 20 to line 35, include dependencies
```

## Step 3: Replace Symbol Content
**Description**: Use precise replacement functionality to update symbol content
**Replacement Requirements**:
- Match original content exactly (including whitespace and indentation)
- Replace with new content maintaining indentation structure
- Perform complete symbol replacement, not partial

**Core Requirements**:
1. **Exact Match**: Original content must match completely including whitespace and indentation
2. **Preserve Indentation**: New content must maintain same indentation level
3. **Complete Symbol**: Replace entire symbol content, not fragments

**Language-Specific Examples**:

### Python
```
→ Use exact text replacement:
Original: "    def login(self, password):\n        return bcrypt.check(password, self.password_hash)"
New:      "    def login(self, password):\n        if not password:\n            return False\n        return bcrypt.check(password, self.password_hash) and self.is_active"
```

### Ruby
```
→ Use exact text replacement:
Original: "  def authenticate(password)\n    BCrypt::Password.new(password_hash) == password\n  end"
New:      "  def authenticate(password)\n    return false if password.blank?\n    BCrypt::Password.new(password_hash) == password && active?\n  end"
```

### Java
```
→ Use exact text replacement:
Original: "    public boolean authenticate(String password) {\n        return BCrypt.checkpw(password, this.passwordHash);\n    }"
New:      "    public boolean authenticate(String password) {\n        if (password == null || password.isEmpty()) {\n            return false;\n        }\n        return BCrypt.checkpw(password, this.passwordHash) && this.isActive();\n    }"
```

### JavaScript/TypeScript
```
→ Use exact text replacement:
Original: "  async authenticate(password) {\n    return bcrypt.compare(password, this.passwordHash);\n  }"
New:      "  async authenticate(password) {\n    if (!password) {\n      return false;\n    }\n    return await bcrypt.compare(password, this.passwordHash) && this.isActive;\n  }"
```

## Step 4: Validate Changes
**Description**: Check syntax errors and validate code integrity after replacement
**Validation Requirements**:
- Check for compile or syntax errors
- Verify code completeness
- Report validation results

**Language-Specific Examples**:
```
# Python
→ Check errors in file "/absolute/path/to/user.py"

# Ruby
→ Check errors in file "/absolute/path/to/user.rb"

# Java
→ Check errors in file "/absolute/path/to/User.java"

# JavaScript
→ Check errors in file "/absolute/path/to/userService.js"
```

## Complete Workflow Examples

### Python Example: "Replace method authenticate in AuthService to add logging"

#### Step 1: Find symbol
```
Search "def authenticate" within AuthService scope,
filter method type, keywords: "authenticate,AuthService"
```

#### Step 2: Read current implementation
```
Read file "src/services/auth_service.py"
from line 45 to line 60,
include dependencies
```

#### Step 3: Replace with new implementation
```
Replace in file "/absolute/path/to/auth_service.py":

Original content:
"    def authenticate(self, username, password):\n        user = self.user_repo.find_by_username(username)\n        if user and user.verify_password(password):\n            return self.create_session(user)\n        return None"

New content:
"    def authenticate(self, username, password):\n        logger.info(f\"Authentication attempt for user: {username}\")\n        user = self.user_repo.find_by_username(username)\n        if user and user.verify_password(password):\n            logger.info(f\"Authentication successful for user: {username}\")\n            return self.create_session(user)\n        logger.warning(f\"Authentication failed for user: {username}\")\n        return None"
```

### Ruby Example: "Replace method calculate_total in class Order"

#### Step 1: Find symbol
```
Search "def calculate_total" within Order scope,
filter method type, keywords: "calculate_total,Order"
```

#### Step 2: Read current implementation
```
Read file "app/models/order.rb"
from line 25 to line 35,
include dependencies
```

#### Step 3: Replace with new implementation
```
Replace in file "/absolute/path/to/order.rb":

Original content:
"  def calculate_total\n    items.sum(&:price)\n  end"

New content:
"  def calculate_total\n    subtotal = items.sum(&:price)\n    tax = subtotal * tax_rate\n    subtotal + tax + shipping_cost\n  end"
```

## Error Prevention

### 1. Exact Text Matching
- Always copy exact text including all whitespace
- Pay attention to tabs vs spaces
- Include complete symbol definition

### 2. Indentation Preservation
- Maintain same indentation level
- Use same indentation style (tabs/spaces)
- Align with surrounding code

### 3. Scope Boundaries
- Replace complete symbol implementation
- Don't break symbol boundaries
- Preserve class/function structure

### 4. Context Awareness
- Check dependencies before replacement
- Ensure imports are available
- Maintain API compatibility

This workflow replaces ReplaceSymbolBodyTool functionality using available LLM tools while ensuring accuracy and safety.