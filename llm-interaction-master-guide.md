# 🤖 Flow-Bento LLM Interaction Master Guide

## 🎯 Core LLM Behaviors

### 📖 **Intelligent File Reading Protocol**

When LLM encounters file reading tasks:

#### Phase 1: Pre-Read Analysis
```
1. 🔍 ANALYZE: What information is needed from this file?
2. 📊 ASSESS: File size and complexity estimation
3. 🎯 STRATEGY: Choose optimal reading approach
```

#### Phase 2: Smart Reading Strategy
```
🔬 SMALL FILES (<500 lines):
→ Read entire file with dependencies context

📚 MEDIUM FILES (500-2000 lines):
→ Read in logical sections (classes, functions)
→ Use symbol overview first, then targeted reads

📖 LARGE FILES (2000+ lines):
→ Symbol overview → Target specific sections
→ Read only relevant portions based on task
```

#### Phase 3: Dependency Context Building
```
🔗 ALWAYS after reading a file:
1. Identify imported modules/dependencies
2. Map function/class relationships
3. Note external API calls or references
4. Store architectural insights in memory
```

### 🔍 **Advanced Symbol Discovery Protocol**

#### Smart Search Sequence:
```
🎯 USER REQUEST: "Find where method login is used"

📋 LLM AUTO-SEQUENCE:
1. find-symbol.md → Locate login method definition
2. find-references.md → Find all usage locations  
3. read-file.md → Read each usage context
4. symbols-overview.md → Understand calling patterns
5. write-memory.md → Store usage patterns discovered
```

#### Cross-Reference Analysis:
```
🧬 DEEP ANALYSIS PATTERN:
1. 📍 LOCATE: Find primary symbol
2. 🌐 MAP: Discover all references and dependencies
3. 📈 ANALYZE: Understanding usage patterns and flow
4. 🧠 SYNTHESIZE: Create comprehensive understanding
5. 💾 STORE: Save architectural insights
```

### 🔄 **Intelligent Workflow Chaining**

#### Decision Tree for Complex Tasks:
```
❓ "Modify user authentication system"

🤖 LLM DECISION PROCESS:
┌─ Is this a SEARCH task? → find-symbol workflows
├─ Is this a MODIFY task? → read → analyze → replace
├─ Is this COMPLEX? → break into sub-tasks
└─ Does it need VALIDATION? → thinking workflows

🔗 AUTO-CHAIN RESULT:
1. think-about-task-adherence.md (understand scope)
2. find-symbol.md (locate auth components) 
3. find-references.md (map all usage)
4. read-file.md (understand current implementation)
5. symbols-overview.md (grasp architecture)
6. replace-symbol.md (implement changes)
7. think-about-whether-you-are-done.md (validate)
8. write-memory.md (document changes)
```

### 🧠 **Context-Aware Memory Management**

#### Automatic Memory Creation Triggers:
```
🎯 ALWAYS CREATE MEMORY WHEN:
- 🏗️ Discovering new architectural patterns
- 🔗 Finding complex dependency relationships  
- 🎨 Learning user's coding style preferences
- 🐛 Identifying common bug patterns
- ⚡ Finding performance optimization opportunities
- 🔒 Discovering security-related code patterns
```

#### Memory Categorization Strategy:
```
📚 MEMORY CATEGORIES:
├── 🏗️ architecture_insights
├── 🔗 dependency_maps  
├── 🎨 coding_patterns
├── 🐛 bug_patterns
├── ⚡ performance_notes
├── 🔒 security_findings
└── 👤 user_preferences
```

## 🚀 **Advanced LLM Automation Rules**

### 🎯 **Smart Context Building**
```
FOR EVERY DEVELOPMENT TASK:
1. 📊 Build dependency map first
2. 🧠 Access relevant memories  
3. 🎯 Apply appropriate workflow chain
4. 💾 Store new insights discovered
5. ✅ Validate with thinking workflows
```

### 🔄 **Failure Recovery Protocol**
```
IF WORKFLOW FAILS:
1. 🛑 STOP current chain
2. 🔍 ANALYZE failure point
3. 📖 CHECK alternative workflows
4. 🔄 RETRY with adjusted approach
5. 💾 STORE recovery pattern for future
```

### ⚡ **Performance Optimization**
```
🚀 SPEED OPTIMIZATIONS:
- 💾 Cache frequently accessed symbol locations
- 🧠 Remember user's common request patterns
- 🔗 Pre-load related workflows for complex tasks
- 📊 Build incremental project understanding
```

---

**🍱 This master guide transforms LLMs into intelligent, context-aware development partners that learn and adapt with every interaction!**