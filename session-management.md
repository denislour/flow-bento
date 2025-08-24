# 🧠 Flow-Bento Session Management

## 🎯 **Session State Tracking for LLMs**

**🤖 LLMs MUST maintain these session variables:**

### 📊 **Core Session Variables**
```javascript
// Session State (maintain throughout conversation)
flowBentoEnabled: boolean = false
lastWorkflowUsed: string = null
sessionMemories: array = []
userPreferences: object = {}
projectContext: object = {}
```

### 🔄 **State Management Rules**

#### **When @bento enable:**
```
flowBentoEnabled = true
→ Apply workflows automatically for ALL development tasks
→ Create session memory: "Flow-Bento enabled by user command"
→ Start proactive memory creation
→ Begin automatic workflow detection
```

#### **When @bento disable:**  
```
flowBentoEnabled = false
→ Stop automatic workflow application
→ Work in standard assistance mode
→ Create session memory: "Flow-Bento disabled by user command"
→ Still respond to @bento commands
```

#### **When @bento <prompt>:**
```
temporaryEnable = true (for this request only)
→ Enable Flow-Bento for this specific task
→ Apply appropriate workflow
→ Return to previous state after completion
→ Create memory of workflow execution
```

## 🎭 **Behavior Modes**

### 🟢 **ENABLED Mode Behavior:**
```
✅ AUTO-DETECT task types:
- Code finding → symbol-analysis workflows
- Code modification → replace workflows
- File operations → file-operations workflows  
- Project tasks → project-management workflows

✅ AUTO-APPLY workflow processes:
- Read appropriate .md file
- Follow 4-step workflow structure
- Create memories proactively
- Use thinking workflows for validation

✅ AUTO-CHAIN workflows for complex tasks:
- find → read → modify → validate → remember
```

### 🔴 **DISABLED Mode Behavior:**
```
❌ NO automatic workflow application
❌ NO proactive memory creation
❌ NO automatic task type detection

✅ STILL respond to direct @bento commands
✅ STILL maintain session awareness
✅ STILL can execute @bento <prompt> requests
```

## 📝 **Session Memory Management**

### **Memory Categories to Track:**
```
🏗️ Project Architecture Insights
- Code structure discoveries
- Dependency mappings
- Pattern identifications

🎯 User Preferences  
- Preferred workflows
- Communication style
- Task complexity preferences

🔄 Workflow Execution History
- Which workflows were successful
- Common task patterns
- Performance optimizations

💡 Session Context
- Current project understanding
- Active development goals
- Previous conversation context
```

### **Memory Creation Triggers:**
```
🎯 WHEN to create session memories:
- After successful workflow execution
- When discovering new project patterns
- After @bento command usage
- When learning user preferences
- After complex workflow chains
```

## 🔍 **Session Context Building**

### **Continuous Context Accumulation:**
```
📊 Throughout session:
1. Track which workflows are most effective
2. Learn user's preferred interaction style
3. Build incremental project understanding
4. Identify recurring task patterns
5. Optimize workflow selection based on history
```

### **Smart Context Application:**
```
🧠 Use session context for:
- Faster workflow selection
- Better task type detection
- Personalized response style
- Improved memory relevance
- Optimized workflow chaining
```

## 🎪 **Response Style Management**

### **ENABLED Response Style:**
```
🍱 Use bento metaphors and structure
🔄 Show workflow process steps
💾 Mention memory creation
✅ Include validation steps
🎯 Focus on organized, methodical approach
```

### **DISABLED Response Style:**
```
💬 Standard conversational assistance
🔧 Direct tool usage without workflow structure
📝 Basic responses without memory creation
⚡ Faster, less structured approach
```

## 🚨 **Critical Session Rules**

### **MUST REMEMBER:**
```
✅ Session state persists across messages
✅ @bento commands change behavior mode
✅ Create memories for significant discoveries
✅ Maintain project context throughout session
✅ Apply user preferences consistently
```

### **MUST NOT:**
```
❌ Forget session state between messages
❌ Apply workflows when disabled (except @bento <prompt>)
❌ Lose track of user preferences
❌ Reset context unnecessarily
❌ Ignore previous workflow execution results
```

## 📊 **Session Status Reporting**

### **When user asks @bento status:**
```
🍱 Flow-Bento Status: [ENABLED/DISABLED]
📂 Available workflows: [count from workflow scan]
💾 Session memories created: [count]
🎯 Last workflow used: [workflow-name]
⏱️ Session duration: [time since first interaction]
🎨 User preferences learned: [list key preferences]
```

## 🔄 **Session Optimization**

### **Performance Improvements:**
```
🚀 Cache frequently used workflows
🧠 Pre-load user's common patterns  
📊 Optimize workflow selection based on history
🎯 Personalize responses based on session learning
⚡ Reduce redundant memory creation
```

### **Learning Patterns:**
```
📈 Track success rates of different workflows
🎯 Identify user's preferred workflow styles
🔄 Learn optimal workflow chaining patterns
💡 Discover project-specific optimizations
```

---

**🧠 This session management ensures consistent, personalized Flow-Bento experiences that improve over time!**