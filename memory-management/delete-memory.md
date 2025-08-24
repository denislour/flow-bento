# Delete Memory

## Function Description (Replaces DeleteMemoryTool)

When user explicitly requests to remove a memory from the project-specific memory store, execute the following workflow to safely delete stored information:

## Step 1: Validate Deletion Request
**Description**: Confirm the deletion is explicitly requested by user
**Requirements**:
- User must explicitly request memory deletion
- Cannot delete memories based on assumptions
- Should only happen when user indicates information is incorrect or irrelevant
- Confirm memory name is correctly specified

**Valid Deletion Scenarios**:
```
# User explicit requests
✅ "Delete the project_setup memory, it's outdated"
✅ "Remove the old_api_docs memory, we don't need it anymore"
✅ "The database_schema memory has wrong information, please delete it"

# Invalid automatic deletions
❌ Deleting memories without user request
❌ Removing memories based on assumptions
❌ Cleaning up memories proactively
```

## Step 2: Verify Memory Exists
**Description**: Check that the specified memory exists before attempting deletion
**Verification Process**:
- Confirm memory name exists in storage
- Check memory is accessible for deletion
- Validate proper permissions for deletion operation

**Verification Examples**:
```
# Memory exists
Request: Delete "outdated_config"
→ Check: ✅ Memory "outdated_config" found
→ Status: Ready for deletion

# Memory not found  
Request: Delete "nonexistent_memory"
→ Check: ❌ Memory "nonexistent_memory" not found
→ Action: Return error message

# Permission check
Request: Delete "protected_memory"
→ Check: ✅ Memory exists, ❌ No deletion permission
→ Action: Return permission error
```

## Step 3: Perform Safe Deletion
**Description**: Remove the memory file from storage safely
**Deletion Process**:
- Remove memory file from project storage
- Clean up any associated metadata
- Ensure no orphaned references remain
- Confirm successful deletion

**Safety Measures**:
```
# Safe deletion practices
→ Verify file exists before deletion
→ Use atomic deletion operations
→ Clean up metadata properly
→ Handle deletion errors gracefully

# Deletion confirmation
→ Confirm file removal successful
→ Verify storage consistency
→ Return success status
```

## Step 4: Confirm Deletion Result
**Description**: Provide confirmation of successful deletion or error details
**Result Reporting**:
- Confirm successful deletion with memory name
- Report any errors that occurred during deletion
- Provide guidance for any issues encountered

**Standard Success Response**:
```
"Memory 'memory_name' has been successfully deleted from the project memory store."
```

**Error Response Examples**:
```
"Error: Memory 'memory_name' not found in the project memory store."
"Error: Permission denied - cannot delete memory 'memory_name'."
"Error: Deletion failed due to storage system error."
```

## Complete Workflow Examples

### Example 1: Delete Outdated Configuration
**Request**: "Delete the old_database_config memory, it's completely outdated"

#### Step 1: Validate request
```
User request: ✅ Explicit deletion request
Reason: "completely outdated"
Target: "old_database_config"
Authorization: User-initiated
```

#### Step 2: Verify memory
```
Check memory: "old_database_config"
Status: ✅ Found in memory store
Size: 1.8KB
Permissions: ✅ Deletion allowed
```

#### Step 3: Perform deletion
```
Action: Delete memory file "old_database_config"
Process: Remove from storage
Cleanup: Clear metadata
Result: ✅ Deletion successful
```

#### Step 4: Confirm result
```
Response: "Memory 'old_database_config' has been successfully deleted from the project memory store."
```

### Example 2: Delete Non-existent Memory
**Request**: "Delete the nonexistent_memory file"

#### Step 1: Validate request
```
User request: ✅ Explicit deletion request
Target: "nonexistent_memory"
```

#### Step 2: Verify memory
```
Check memory: "nonexistent_memory"
Status: ❌ Not found in memory store
```

#### Step 3: Return error
```
Response: "Error: Memory 'nonexistent_memory' not found in the project memory store."
```

### Example 3: Delete Incorrect Documentation
**Request**: "The api_v1_docs memory has wrong information, please remove it"

#### Step 1: Validate request
```
User request: ✅ Explicit deletion request
Reason: "has wrong information"
Target: "api_v1_docs"
```

#### Step 2: Verify and delete
```
Memory found: ✅ "api_v1_docs"
Deletion: ✅ Successful
```

#### Step 3: Confirm
```
Response: "Memory 'api_v1_docs' has been successfully deleted from the project memory store."
```

## When to Delete Memories

### Valid Deletion Reasons
```
# Outdated information
✅ Technology stack has changed completely
✅ API documentation is for deprecated version
✅ Configuration no longer applies to project

# Incorrect information
✅ Memory contains factual errors
✅ Procedures documented are incorrect
✅ Information leads to problems

# No longer relevant
✅ Feature was removed from project
✅ Process is no longer used
✅ Information applies to different project

# User explicit request
✅ User specifically asks for deletion
✅ User indicates information is harmful
✅ User wants to replace with updated version
```

### Invalid Deletion Scenarios
```
❌ Automatic cleanup without user request
❌ Removing memories to save space
❌ Deleting based on assumptions about relevance
❌ Removing memories during routine maintenance
❌ Deleting to prevent confusion (without user request)
```

## Best Practices

### 1. Require Explicit User Request
```
✅ Only delete when user explicitly requests
✅ Confirm user wants specific memory deleted
✅ Ask for clarification if request is ambiguous
✅ Respect user's decision about memory management

❌ Delete memories proactively
❌ Assume user wants outdated memories removed
❌ Clean up memories without permission
❌ Delete based on your assessment of relevance
```

### 2. Verify Before Deletion
```
✅ Confirm memory exists before attempting deletion
✅ Check permissions and access rights
✅ Validate memory name spelling and format
✅ Ensure deletion is technically possible

❌ Attempt deletion without verification
❌ Assume memory exists based on name
❌ Skip permission checks
❌ Ignore potential technical issues
```

### 3. Handle Errors Gracefully
```
✅ Provide clear error messages
✅ Suggest alternative actions when appropriate
✅ Help user identify correct memory names
✅ Explain permission or technical issues

❌ Fail silently on errors
❌ Provide confusing error messages
❌ Leave user unsure about deletion status
❌ Ignore or hide technical problems
```

### 4. Confirm Results
```
✅ Always confirm successful deletion
✅ Provide clear success messages
✅ Include memory name in confirmation
✅ Indicate deletion is permanent

❌ Delete without confirmation
❌ Leave user unsure about results
❌ Provide ambiguous status messages
❌ Fail to indicate permanence of action
```

## Integration with Memory Management

### Memory Lifecycle Management
```
1. Creation → User creates memory with useful information
2. Usage → Memory is read and referenced during development
3. Updates → Memory content is modified when information changes
4. Deletion → Memory is removed when explicitly requested by user
```

### Before Deletion Alternatives
```
# Consider alternatives before deletion
✅ Update memory with correct information
✅ Rename memory to be more accurate
✅ Merge with other relevant memories
✅ Archive memory instead of deleting

# Only delete when
✅ User explicitly requests deletion
✅ Information is completely irrelevant
✅ Memory cannot be corrected or updated
✅ User prefers to start fresh
```

### Post-Deletion Considerations
```
# After successful deletion
→ Memory is permanently removed
→ Information cannot be recovered
→ User may need to recreate if needed later
→ Consider documenting why deletion occurred
```

## Error Handling

### Memory Not Found
```
Error Message: "Error: Memory 'memory_name' not found in the project memory store."

Possible Causes:
- Memory name is misspelled
- Memory was already deleted
- Memory never existed
- Working in wrong project context

Solutions:
- Use list_memories to see available memories
- Check spelling of memory name
- Verify project context is correct
```

### Permission Denied
```
Error Message: "Error: Permission denied - cannot delete memory 'memory_name'."

Possible Causes:
- Insufficient user permissions
- Memory is protected or read-only
- System-level access restrictions

Solutions:
- Contact project administrator
- Check user permissions
- Verify memory is not system-protected
```

### Storage System Error
```
Error Message: "Error: Deletion failed due to storage system error."

Possible Causes:
- File system issues
- Storage full or corrupted
- Concurrent access conflicts

Solutions:
- Retry deletion operation
- Check system resources
- Contact technical support if persistent
```

## Safety Considerations

### Permanent Action Warning
```
⚠️  Memory deletion is PERMANENT
⚠️  Deleted information cannot be recovered
⚠️  Consider updating instead of deleting
⚠️  Ensure user really wants deletion
```

### User Confirmation
```
# Before deletion, ensure:
✅ User explicitly requested deletion
✅ User understands deletion is permanent
✅ User provided specific memory name
✅ Reason for deletion is clear

# Do not delete if:
❌ User only mentioned memory is outdated
❌ Request is ambiguous or unclear
❌ User seems unsure about deletion
❌ No explicit deletion instruction
```

### Documentation Impact
```
# Consider impact of deletion:
→ Will other team members need this information?
→ Could updated version be more helpful than deletion?
→ Is this information referenced elsewhere?
→ Should deletion be documented for project history?
```

This workflow replaces DeleteMemoryTool functionality for safely removing memories from the project memory store only when explicitly requested by users.