# Debugging Runtime Errors with GitHub Copilot

## Prompt 1: Troubleshooting Common Runtime Errors
```
Intent: To help developers debug runtime errors using GitHub Copilot.

Context: You are debugging a runtime error in your code. The error details are as follows:

programming_language: {programming_language}
error_message: {error_message}
code_snippet: {code_snippet}
execution_environment: {execution_environment}

Analyze the error and provide:
- Explanation of the error
- Potential causes
- Code fixes with clear explanations
- Prevention tips

Example:
programming_language: "JavaScript"
error_message: "TypeError: Cannot read property 'name' of undefined"
code_snippet: 
```javascript
function displayUserInfo(user_data) {
  const user_name = user_data.name;
  const user_email = user_data.email;
  
  console.log(`User: ${user_name}, Email: ${user_email}`);
  
  if (user_data.preferences.notifications) {
    console.log("Notifications: Enabled");
  } else {
    console.log("Notifications: Disabled");
  }
}

// Function call
const user_id = getUserIdFromUrl();
const user_data = fetchUserData(user_id);
displayUserInfo(user_data);
```
execution_environment: "Node.js v16.13.0"

Analysis:
The error "TypeError: Cannot read property 'name' of undefined" indicates you're trying to access a property ('name') on an undefined value. In this code, it's likely happening because:

1. `user_data` is undefined when passed to `displayUserInfo()`
2. This could occur if `fetchUserData(user_id)` fails to return user data, perhaps due to:
   - Network request failure
   - User not found
   - Asynchronous code issue (not awaiting a Promise)

Additionally, even if `user_data` exists, accessing `user_data.preferences.notifications` could cause a similar error if `preferences` is undefined.

Potential Fixes:

1. Add null checks to prevent accessing properties on undefined objects:

```javascript
function displayUserInfo(user_data) {
  // Check if user_data exists before accessing properties
  if (!user_data) {
    console.error("User data is undefined");
    return;
  }
  
  const user_name = user_data.name || "Unknown";
  const user_email = user_data.email || "No email";
  
  console.log(`User: ${user_name}, Email: ${user_email}`);
  
  // Use optional chaining to safely access nested properties
  if (user_data.preferences?.notifications) {
    console.log("Notifications: Enabled");
  } else {
    console.log("Notifications: Disabled");
  }
}
```

2. If `fetchUserData` is asynchronous, ensure you're properly handling the Promise:

```javascript
// Using async/await
async function loadAndDisplayUserInfo() {
  try {
    const user_id = getUserIdFromUrl();
    const user_data = await fetchUserData(user_id);
    displayUserInfo(user_data);
  } catch (error) {
    console.error("Error loading user data:", error);
  }
}

// Or using Promises
function loadAndDisplayUserInfo() {
  const user_id = getUserIdFromUrl();
  fetchUserData(user_id)
    .then(user_data => {
      displayUserInfo(user_data);
    })
    .catch(error => {
      console.error("Error loading user data:", error);
    });
}
```

Prevention Tips:
1. Always validate input parameters at the beginning of functions
2. Use optional chaining (`?.`) for accessing potentially undefined nested properties
3. Provide default values using the nullish coalescing operator (`??`) or logical OR (`||`)
4. Properly handle asynchronous operations with try/catch or .then()/.catch()
5. Implement proper error handling throughout your application
```

## Prompt 2: Debugging Patterns with GitHub Copilot

### Debugging Strategy Template
```markdown
Intent: To guide systematic debugging using GitHub Copilot.

Context: You are debugging an issue in your code. Describe:
- Error symptoms
- Reproduction steps
- Environment details
- Recent changes

Example debugging flow:
error_type: "Runtime Exception"
symptoms: "Application crashes when processing large files"
environment: "Production server"
recent_changes: "Added parallel processing feature"
```

### Common Debugging Patterns

1. **Error Analysis Pattern**
```typescript
/**
 * Debug pattern for runtime errors:
 * 1. Log error details
 * 2. Check stack trace
 * 3. Analyze variable state
 * 4. Test hypotheses
 */
function debug_error_state(error: Error) {
    console.log({
        error_name: error.name,
        message: error.message,
        stack: error.stack,
        timestamp: new Date().toISOString()
    });

    // Additional context
    console.log({
        memory_usage: process.memoryUsage(),
        active_connections: server.connections.length,
        system_state: getCurrentState()
    });
}
```

2. **State Tracking Pattern**
```typescript
/**
 * Track state changes for debugging:
 * - Variable values
 * - Function calls
 * - State transitions
 * - Timing information
 */
class StateTracker {
    private state_log: any[] = [];
    
    track_state(context: string, data: any) {
        this.state_log.push({
            context,
            data,
            timestamp: Date.now(),
            stack: new Error().stack
        });
    }

    get_state_history() {
        return this.state_log;
    }
}
```

### Debug Logging Patterns

1. **Structured Logging**
```typescript
/**
 * Implement structured logging for debugging:
 * - Consistent format
 * - Required context
 * - Correlation IDs
 * - Performance metrics
 */
interface DebugLog {
    level: 'debug' | 'info' | 'warning' | 'error';
    message: string;
    context: {
        function_name: string;
        correlation_id: string;
        user_id?: string;
        timing_ms?: number;
    };
    data?: any;
}
```

2. **Performance Debugging**
```typescript
/**
 * Debug performance issues:
 * - Timing measurements
 * - Resource usage
 * - Bottleneck detection
 * - Memory patterns
 */
class PerformanceDebugger {
    start_time: number;
    measurements: Map<string, number[]>;

    measure_execution(operation: string, fn: Function) {
        const start = performance.now();
        const result = fn();
        const duration = performance.now() - start;
        
        this.record_measurement(operation, duration);
        return result;
    }
}
```

### Error Recovery Patterns

1. **Graceful Degradation**
```typescript
/**
 * Implement recovery strategies:
 * - Fallback options
 * - Retry logic
 * - Circuit breakers
 * - State restoration
 */
class ErrorRecovery {
    async with_fallback<T>(
        primary: () => Promise<T>,
        fallback: () => Promise<T>,
        max_retries: number = 3
    ): Promise<T> {
        try {
            return await this.with_retry(primary, max_retries);
        } catch (error) {
            console.warn(`Primary operation failed, using fallback`, { error });
            return await fallback();
        }
    }
}
```

2. **State Recovery**
```typescript
/**
 * Recover from error states:
 * - Backup data
 * - Restore points
 * - Cleanup operations
 * - Validation checks
 */
class StateRecovery {
    async restore_state(checkpoint_id: string) {
        const checkpoint = await load_checkpoint(checkpoint_id);
        await validate_state(checkpoint);
        await apply_state(checkpoint);
    }
}
```

### Debugging Best Practices

1. **Systematic Approach**
   - Gather all relevant information
   - Form and test hypotheses
   - Document findings
   - Verify fixes

2. **Tool Integration**
   - Use debugging tools effectively
   - Integrate logging systems
   - Monitor system metrics
   - Track error patterns

3. **Prevention Strategies**
   - Add validation checks
   - Implement monitoring
   - Use type safety
   - Handle edge cases

### Anti-patterns to Avoid

1. **Debugging Pitfalls**
   - Console.log debugging in production
   - Incomplete error handling
   - Ignoring error patterns
   - Missing root cause analysis

2. **Process Issues**
   - No reproduction steps
   - Incomplete documentation
   - Untested fixes
   - Ignored warning signs