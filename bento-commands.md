## 📝 **Symbol Usage Clarification**

### 🎨 **Command Symbol Hierarchy:**
```
🔥 *bento commands: Core Flow-Bento control commands
→ Examples: *bento enable, *bento disable, *bento <prompt>

⚡ **commands: Advanced/custom commands (future expansion)
→ Examples: **analyze, **optimize, **debug

📝 /* comments */: Internal LLM processing notes
→ Examples: /* workflow applied */, /* memory created */

🚨 IMPORTANT: 
- *bento symbols are for Flow-Bento control only
- ** symbols reserved for advanced custom commands
- /* */ symbols for internal comments/notes
```

### 🎯 **Usage Guidelines:**
- ***bento**: User types these to control Flow-Bento
- ****commands**: Reserved for future advanced features
- **/* comments */**: LLM internal processing notes
- **// comments**: Code-style comments in workflows

# 🍱 *bento Command System 

## 🎯 **LLM Command Detection Protocol**

**🤖 LLMs: When you see *bento commands, follow these instructions exactly!**

### 📋 **Command Detection Pattern:**
```
IF user message starts with "*bento" → Process as bento command
IF user message contains "*bento <prompt>" → Enable + Execute prompt
IF user message starts with "**" → Process as custom advanced command
```

## 🔧 ***bento Commands Reference**

### 1. ***bento enable** 
```
🚀 ACTION: Activate Flow-Bento system
📖 RESPONSE: 
"✅ Flow-Bento system ENABLED! 🍱
🔄 All development tasks will now use structured workflows
📚 Type '@bento help' for available commands"

🎯 BEHAVIOR: 
- Read enable.md immediately
- Activate all workflow auto-detection
- Create session memory: "Flow-Bento enabled by user command"
```

### 2. ***bento disable**
```
🛑 ACTION: Deactivate Flow-Bento system  
📖 RESPONSE:
"❌ Flow-Bento system DISABLED
🔄 Reverting to standard development assistance
💡 Type '@bento enable' to reactivate workflows"

🎯 BEHAVIOR:
- Stop automatic workflow application
- Work in standard mode
- Create session memory: "Flow-Bento disabled by user command"
```

### 3. ***bento <prompt>**
```
🚀 ACTION: Enable + Execute with Flow-Bento
📖 RESPONSE:
"🍱 Flow-Bento ACTIVE for this request!
🔄 Applying appropriate workflows..."

🎯 BEHAVIOR:
1. Auto-enable Flow-Bento if not already active
2. Analyze the <prompt> for task type
3. Apply appropriate workflow automatically:
   - Code finding → symbol-analysis workflows
   - Code modification → replace workflows  
   - File operations → file-operations workflows
   - Project analysis → project-management workflows
4. Execute with full workflow process
5. Create memory of workflow execution
```

### 4. ***bento help**
```
📚 ACTION: Show available commands
📖 RESPONSE: Display command reference and status
```

### 5. ***bento status**
```
📊 ACTION: Show current Flow-Bento status
📖 RESPONSE: 
"🍱 Flow-Bento Status: [ENABLED/DISABLED]
📂 Available workflows: [count] 
💾 Session memories: [count]
🎯 Last workflow used: [workflow-name]"
```

### 6. ***bento workflows**
```
📋 ACTION: List available workflow categories
📖 RESPONSE: Show all workflow compartments with descriptions
```

## 🎯 **Session Management**

### **Session State Tracking:**
```
🧠 LLM MUST remember:
- Flow-Bento enabled/disabled status
- Last used workflows in session  
- User preferences for workflow application
- Session-specific memories created
```

### **State Persistence:**
```
✅ ENABLED STATE:
- Apply workflows automatically for ALL development tasks
- Create memories proactively
- Use thinking workflows for validation

❌ DISABLED STATE:  
- Work in standard mode (no automatic workflows)
- Still respond to direct @bento commands
- Don't auto-apply workflow processes
```

## 🔄 **Workflow Integration with Commands**

### **@bento + Task Detection:**
```
Example: "@bento find the User class in this project"

🔄 LLM AUTO-PROCESS:
1. Detect "@bento" → Enable Flow-Bento  
2. Parse "find the User class" → symbol-analysis task
3. Auto-apply: symbol-analysis/find-symbol.md
4. Execute 4-step workflow process
5. Create memory: "Found User class at [location]"
6. Maintain enabled state for session
```

### **Smart Context Building:**
```
🧠 WHEN @bento enabled:
- Build comprehensive project context
- Apply cross-reference analysis
- Use intelligent workflow chaining
- Create architectural insights
- Proactive memory management

🎯 WHEN @bento disabled:
- Standard assistance mode
- No automatic workflow application
- Respond to commands but don't chain workflows
```

## 📝 **Response Templates**

### **Enable Response:**
```
"🍱 **Flow-Bento ENABLED!** 
✅ Structured workflows now active for all development tasks
🔄 Your requests will be processed with intelligent workflow automation
📚 Available commands: @bento help | @bento status | @bento disable

🎯 Ready to assist with mindful, organized development! What shall we cook today?"
```

### **Disable Response:**  
```
"❌ **Flow-Bento DISABLED**
🔄 Switched to standard development assistance mode
💡 Workflows can be reactivated with: @bento enable
🍱 @bento <prompt> still works for one-time workflow execution"
```

### **Workflow Execution Response:**
```
"🍱 **Flow-Bento Active!** Applied [workflow-name]
📋 Process: [Step 1] → [Step 2] → [Step 3] → [Step 4] ✅
💾 Memory created: [insight summary]
🎯 Result: [workflow output]"
```

## 🚨 **Critical LLM Rules**

### **ALWAYS DO:**
✅ Detect @bento commands at start of user messages
✅ Maintain session state (enabled/disabled) 
✅ Apply workflows when enabled + development task detected
✅ Create session memories for @bento usage
✅ Respond with clear status indicators

### **NEVER DO:**
❌ Ignore @bento commands
❌ Apply workflows when disabled (except @bento <prompt>)
❌ Forget session state between messages
❌ Skip memory creation for workflow executions

## 🎯 **Success Indicators**

User will know @bento system works when:
- ✅ @bento enable activates structured workflow responses
- ✅ @bento disable stops automatic workflow application  
- ✅ @bento <prompt> applies workflows for that specific request
- ✅ Development tasks get workflow treatment when enabled
- ✅ Clear status indicators show current state

---

**🍱 This command system gives users complete control over when and how Flow-Bento workflows are applied!**