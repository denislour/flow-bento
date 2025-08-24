# Think About Task Adherence

## Function Description (Replaces ThinkAboutTaskAdherenceTool)

Before making any code changes (insert, replace, or delete operations), execute the following workflow to ensure you remain focused on the original task and haven't drifted from the user's requirements:

## Step 1: Review Original Task Requirements
**Description**: Revisit the initial user request to understand core objectives
**Review Process**:
- Re-read the original user request carefully
- Identify the primary goals and objectives
- Note any specific requirements or constraints mentioned
- Understand the scope and boundaries of the task

**Task Analysis Framework**:
```
# Core task identification
→ What is the main problem to solve?
→ What specific outcome does the user want?
→ Are there multiple sub-tasks involved?
→ What are the success criteria?

# Requirement extraction
→ Functional requirements (what the code should do)
→ Non-functional requirements (performance, security, etc.)
→ Technical constraints (technology, architecture, etc.)
→ Business constraints (timeline, resources, etc.)

# Scope definition
→ What is explicitly included in the task?
→ What is explicitly excluded?
→ What assumptions are reasonable to make?
→ Where are the boundaries of this work?
```

## Step 2: Assess Current Understanding vs Original Intent
**Description**: Compare your current plan with the original user intentions
**Comparison Analysis**:
- Does your current approach address the core problem?
- Have you maintained focus on the primary objectives?
- Are you solving the right problem?
- Have you expanded the scope inappropriately?

**Alignment Check**:
```
# Well-aligned indicators
✅ Current plan directly addresses user's stated problem
✅ Proposed changes solve the specific issue mentioned
✅ Scope remains within reasonable bounds of request
✅ Approach matches user's expectations and context

# Misalignment indicators
❌ Current plan addresses a different problem
❌ Scope has expanded beyond original request
❌ Focus has shifted to tangential issues
❌ Approach is more complex than necessary
❌ Solution doesn't match user's apparent needs
```

## Step 3: Evaluate Conversation History for Drift
**Description**: Review the conversation progression to identify any drift from original goals
**Drift Analysis**:
- How has the conversation evolved from the initial request?
- Have new requirements been introduced that change the scope?
- Are you addressing issues the user didn't ask about?
- Has the complexity grown beyond the original intent?

**Common Drift Patterns**:
```
# Scope creep
→ Adding features not requested
→ Solving related but different problems
→ Optimizing areas not mentioned by user
→ Addressing potential future needs

# Technical rabbit holes
→ Over-engineering solutions
→ Focusing on implementation details vs outcomes
→ Getting distracted by interesting technical challenges
→ Solving problems that don't need solving

# Assumption drift
→ Making assumptions about unstated requirements
→ Interpreting user needs beyond what they expressed
→ Adding complexity based on perceived best practices
→ Solving for edge cases not mentioned
```

## Step 4: Confirm Current Approach Alignment
**Description**: Validate that your planned code changes align with the task
**Validation Questions**:
- Will the planned changes directly solve the user's problem?
- Are the changes minimal and focused on the core issue?
- Do the changes introduce unnecessary complexity?
- Are you confident this is what the user actually wants?

**Alignment Validation**:
```
# Strong alignment signals
✅ Changes directly address stated problem
✅ Solution is proportional to problem complexity
✅ User requirements are clearly met
✅ Changes are minimal and focused
✅ No additional complexity introduced unnecessarily

# Weak alignment signals
⚠️ Changes solve more than what was asked
⚠️ Solution complexity exceeds problem complexity
⚠️ Unclear if user actually wants these changes
⚠️ Multiple different approaches being considered
⚠️ Changes touch many unrelated areas

# Misalignment signals
❌ Changes don't directly address user's problem
❌ Solution is overly complex for the stated need
❌ Changes expand scope significantly
❌ Approach seems disconnected from original request
```

## Complete Workflow Examples

### Example 1: Well-Aligned Task Progress
**Original Request**: "Fix the login button that's not working on the home page"

#### Step 1: Review requirements
```
Core objective: Fix broken login button functionality
Specific requirement: Button on home page should work
Success criteria: Users can click login button and proceed to login
Scope: Home page login button only
```

#### Step 2: Assess current understanding
```
Current plan: 
- Identified login button component
- Found missing click handler
- Plan to add proper event handler

Alignment check:
✅ Directly addresses broken login button
✅ Focused on home page as specified
✅ Solution is proportional to problem
✅ Minimal change to fix specific issue
```

#### Step 3: Evaluate conversation
```
Conversation progression:
1. User reported broken login button
2. Investigated home page components
3. Found root cause in event handler
4. Planned minimal fix

Drift analysis: ✅ No drift - stayed focused on specific issue
```

#### Step 4: Confirm alignment
```
Planned changes: Add click handler to login button component
Validation:
✅ Directly solves stated problem
✅ Minimal and focused change
✅ No unnecessary complexity
✅ Clearly what user wants

Decision: ✅ PROCEED with code changes
```

### Example 2: Detected Scope Drift
**Original Request**: "Add a search feature to the product listing page"

#### Step 1: Review requirements  
```
Core objective: Add search functionality to product listing
Specific requirement: Search feature on product listing page
Success criteria: Users can search and filter products
Scope: Product listing page search only
```

#### Step 2: Assess current understanding
```
Current plan:
- Redesign entire product listing architecture
- Add advanced filtering with categories, price ranges
- Implement autocomplete with search suggestions
- Add search analytics and tracking
- Optimize database queries for performance

Alignment check:
❌ Plan is much more complex than requested
❌ Includes features not mentioned by user
❌ Scope has expanded significantly beyond "search feature"
```

#### Step 3: Evaluate conversation
```
Conversation progression:
1. User asked for search feature
2. Explored existing product listing code
3. Discovered performance issues
4. Started planning comprehensive improvements
5. Added advanced features "while we're at it"

Drift analysis: ❌ Significant scope drift detected
- Original: simple search feature
- Current: comprehensive product listing redesign
```

#### Step 4: Confirm alignment
```
Planned changes: Complete product listing redesign with advanced features
Validation:
❌ Much more complex than user requested
❌ Includes many features not asked for
❌ Scope significantly expanded
❌ Uncertain if user wants this complexity

Decision: ⚠️ REFOCUS on original simple search requirement
Action: Scale back to basic search functionality only
```

### Example 3: Clarification Needed
**Original Request**: "Improve the user registration process"

#### Step 1: Review requirements
```
Core objective: Improve user registration process
Issue: Request is somewhat vague
Success criteria: Not clearly defined
Scope: User registration, but extent unclear
```

#### Step 2: Assess current understanding
```
Current plan:
- Add email verification
- Improve form validation
- Add password strength requirements
- Redesign registration UI

Alignment check:
⚠️ User didn't specify what "improve" means
⚠️ Multiple possible improvements identified
⚠️ Unclear which improvements user wants
⚠️ May be overengineering without direction
```

#### Step 3: Evaluate conversation
```
Conversation progression:
1. User requested registration improvements
2. Explored current registration code
3. Identified multiple improvement opportunities
4. Started planning comprehensive changes

Drift analysis: ⚠️ Possible scope expansion without clear direction
```

#### Step 4: Confirm alignment
```
Planned changes: Multiple registration improvements
Validation:
⚠️ User request was vague about specific improvements
⚠️ Multiple changes planned without user input
⚠️ Uncertain which improvements are desired
⚠️ Risk of solving wrong problems

Decision: 🤔 CLARIFY requirements with user
Action: Ask user to specify what improvements they want
```

## Task Adherence Principles

### Stay Focused on Core Problem
```
✅ Keep the main user problem as primary focus
✅ Resist the urge to solve related but different problems
✅ Maintain scope discipline throughout implementation
✅ Question each addition: "Did the user ask for this?"

❌ Expand scope without user confirmation
❌ Add features "while we're at it"
❌ Solve problems the user didn't mention
❌ Let technical interests override user needs
```

### Maintain Proportional Complexity
```
✅ Solution complexity should match problem complexity
✅ Simple problems deserve simple solutions
✅ Complex solutions require explicit user approval
✅ Err on the side of simplicity

❌ Over-engineer simple problems
❌ Add unnecessary technical complexity
❌ Implement enterprise solutions for simple needs
❌ Assume user wants the "best" technical solution
```

### Validate Assumptions
```
✅ Question assumptions about unstated requirements
✅ Clarify ambiguous requests before implementing
✅ Confirm scope expansions with user
✅ Validate approach aligns with user expectations

❌ Assume you know what user "really" wants
❌ Implement based on best practices without confirmation
❌ Add features based on assumptions
❌ Proceed with unclear requirements
```

## Common Task Drift Scenarios

### Feature Creep
```
Original: "Add a logout button"
Drift: "Redesign entire authentication system with logout"
Correction: Add simple logout button as requested
```

### Technical Rabbit Holes
```
Original: "Fix slow database query"
Drift: "Redesign entire database architecture"
Correction: Focus on optimizing the specific slow query
```

### Perfectionism
```
Original: "Add basic form validation"
Drift: "Implement comprehensive validation framework"
Correction: Add simple validation for the specific form
```

### Scope Expansion
```
Original: "Fix bug in user profile page"
Drift: "Redesign all user-related pages"
Correction: Fix the specific bug in user profile page
```

## Best Practices

### 1. Regular Alignment Checks
```
✅ Check alignment before major implementation decisions
✅ Question scope expansions immediately
✅ Validate assumptions about user needs
✅ Keep original request visible and referenced

❌ Proceed without alignment validation
❌ Let scope drift accumulate gradually
❌ Make assumptions without validation
❌ Lose sight of original request
```

### 2. User-Centric Focus
```
✅ Prioritize user's stated needs over technical preferences
✅ Solve the problem the user actually has
✅ Choose simplicity over technical elegance when appropriate
✅ Ask for clarification when requirements are unclear

❌ Prioritize technical interests over user needs
❌ Solve problems the user doesn't have
❌ Add complexity for its own sake
❌ Proceed with unclear requirements
```

### 3. Scope Discipline
```
✅ Resist the urge to improve "related" areas
✅ Keep changes minimal and focused
✅ Get explicit approval for scope expansions
✅ Document any scope changes and rationale

❌ Expand scope without user approval
❌ Make changes beyond the requested area
❌ Assume broader changes are wanted
❌ Let technical discoveries drive scope expansion
```

## Integration with Development Process

### Before Code Changes
```
1. Review original task → What did user actually request?
2. Assess current plan → Does it align with the request?
3. Check for drift → Has the scope expanded inappropriately?
4. Validate approach → Is this what the user wants?
5. Proceed or adjust → Make changes or refocus as needed
```

### During Implementation
```
→ Keep original request visible
→ Question each addition or complication
→ Validate alignment at decision points
→ Resist technical tangents
→ Focus on delivering what was requested
```

### Before Completion
```
→ Compare final result with original request
→ Verify all requirements are met
→ Ensure no unnecessary additions were made
→ Confirm scope remained appropriate
→ Validate user will be satisfied with result
```

This workflow replaces ThinkAboutTaskAdherenceTool functionality for ensuring continued alignment with user requirements throughout the development process.