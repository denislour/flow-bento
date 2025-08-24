# Replace Symbol Prompt Template

This template provides structured prompts for LLMs to interact effectively when performing symbol replacement operations.

## 🎯 Standard Replace Symbol Prompt Template

### Template Structure
```
CONTEXT: [Brief description of the modification needed]
TARGET: [Specific symbol to be replaced - class/method/function name]  
SCOPE: [File/directory scope of the change]
REQUIREMENTS: [Specific requirements and constraints]
VALIDATION: [How to verify the change is successful]
```

## 📝 Prompt Templates by Scenario

### Template 1: Method Implementation Update
```
CONTEXT: Update method implementation to improve [functionality/performance/security]
TARGET: Method [method_name] in class [class_name]
SCOPE: File [file_path] or directory [directory_path]
REQUIREMENTS: 
- Maintain existing function signature
- Preserve backward compatibility  
- Follow project coding standards
- Handle edge cases appropriately
VALIDATION:
- Code compiles without errors
- Existing tests still pass
- New functionality works as specified
- No breaking changes to dependent code

WORKFLOW APPLICATION:
1. Apply find-symbol.md to locate target method
2. Apply read-file.md to understand current implementation
3. Apply replace-symbol.md to implement changes safely
4. Apply think-about-whether-you-are-done.md to validate
5. Apply write-memory.md to store insights
```

### Template 2: Class Structure Modification
```
CONTEXT: Modify class structure to add/remove/update [properties/methods]
TARGET: Class [class_name]
SCOPE: File [file_path] and related files
REQUIREMENTS:
- Maintain class interface compatibility
- Update all affected methods
- Preserve existing functionality
- Follow OOP principles and project patterns
VALIDATION:
- Class compiles and instantiates correctly
- All class methods work as expected
- Dependent classes still function properly
- Documentation reflects changes

WORKFLOW APPLICATION:
1. Apply find-symbol.md to locate target class
2. Apply symbols-overview.md to understand class structure  
3. Apply find-references.md to map dependencies
4. Apply replace-symbol.md to modify class safely
5. Apply think-about-whether-you-are-done.md to validate
6. Apply write-memory.md to store architectural insights
```

### Template 3: Function Refactoring
```
CONTEXT: Refactor function to improve [readability/performance/maintainability]
TARGET: Function [function_name]
SCOPE: Function definition and all call sites
REQUIREMENTS:
- Maintain function behavior and output
- Improve internal implementation
- Update all function calls if signature changes
- Maintain or improve performance
VALIDATION:
- Function produces same outputs for same inputs
- All calling code works without modification
- Performance meets or exceeds original
- Code is more readable/maintainable

WORKFLOW APPLICATION:
1. Apply find-symbol.md to locate target function
2. Apply find-references.md to find all usage locations
3. Apply read-file.md to understand current implementation
4. Apply replace-symbol.md to implement refactored version
5. Apply think-about-whether-you-are-done.md to validate
6. Apply write-memory.md to store refactoring patterns
```

### Template 4: Bug Fix Implementation
```
CONTEXT: Fix bug in [specific functionality/behavior]
TARGET: [Symbol/method/function] containing the bug
SCOPE: Affected files and potential side effects
REQUIREMENTS:
- Fix the specific bug without introducing new ones
- Maintain existing functionality for non-bug cases
- Add appropriate error handling
- Follow defensive programming practices
VALIDATION:
- Bug no longer occurs under test conditions
- Existing functionality remains intact
- New error handling works appropriately
- No regression issues introduced

WORKFLOW APPLICATION:
1. Apply find-symbol.md to locate buggy code
2. Apply read-file.md to understand current implementation
3. Apply find-references.md to understand usage patterns
4. Apply replace-symbol.md to implement bug fix
5. Apply think-about-whether-you-are-done.md to validate fix
6. Apply write-memory.md to store bug fix patterns
```

## 🎨 Customizable Prompt Elements

### Context Modifiers
```
# For Performance Issues
CONTEXT: Optimize [symbol] to improve [specific performance metric]

# For Security Fixes  
CONTEXT: Secure [symbol] against [specific vulnerability type]

# For Feature Addition
CONTEXT: Extend [symbol] to support [new functionality]

# For Code Quality
CONTEXT: Refactor [symbol] to improve [code quality aspect]
```

### Requirement Specifications
```
# Compatibility Requirements
- Maintain API compatibility
- Preserve backward compatibility
- Ensure cross-platform compatibility

# Quality Requirements  
- Follow coding standards [specify standards]
- Meet performance benchmarks [specify metrics]
- Maintain test coverage [specify percentage]

# Integration Requirements
- Integrate with existing [systems/frameworks]
- Support current [data formats/protocols]
- Work with existing [dependencies/libraries]
```

### Validation Criteria
```
# Functional Validation
- All existing tests pass
- New functionality works as specified
- Edge cases handled appropriately

# Non-Functional Validation
- Performance meets requirements
- Security standards maintained
- Accessibility standards met

# Integration Validation
- Dependencies still work correctly
- External systems integration intact  
- Data consistency maintained
```

## 🚀 Usage Instructions

### For LLMs Using These Templates:

1. **Select Appropriate Template**: Choose based on modification type
2. **Fill Template Fields**: Replace bracketed placeholders with specific information
3. **Apply Workflow Sequence**: Follow the specified workflow application steps
4. **Create Context Memory**: Store insights using the memory management workflows
5. **Validate Completion**: Use thinking workflows to ensure quality

### For Users Requesting Modifications:

1. **Provide Clear Context**: Explain what needs to be changed and why
2. **Specify Target Precisely**: Identify exact symbols/code elements to modify
3. **Define Requirements**: List any constraints, standards, or compatibility needs
4. **Describe Validation**: Explain how to verify the change is successful

## 📋 Quality Assurance Checklist

### Before Using Template
- [ ] Template matches the type of modification needed
- [ ] All required information available to fill template
- [ ] Scope and requirements clearly defined
- [ ] Validation criteria established

### During Template Application
- [ ] Follow workflow sequence exactly as specified
- [ ] Apply all safety and validation steps
- [ ] Create appropriate context memories
- [ ] Document decisions and insights

### After Template Completion
- [ ] Validate all specified criteria met
- [ ] Test functionality thoroughly
- [ ] Update documentation as needed
- [ ] Store successful patterns for future use

---

**These prompt templates ensure consistent, high-quality symbol replacement operations while maintaining clear communication between users and LLMs.**