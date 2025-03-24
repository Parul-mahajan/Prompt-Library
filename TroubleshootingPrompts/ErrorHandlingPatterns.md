# Error Handling Patterns with GitHub Copilot

## Prompt 1: Implementing Robust Error Handling
```markdown
Intent: To help developers implement comprehensive error handling using GitHub Copilot.

Context: Provide clear guidance for error handling implementation:
- Error types and hierarchies
- Recovery strategies
- Logging patterns
- User feedback

Example:
```typescript
/**
 * Error handling implementation for:
 * System: E-commerce platform
 * Component: Payment processing
 * Requirements:
 * - Handle network errors
 * - Validate input data
 * - Manage timeouts
 * - Provide user feedback
 */
```

### Error Handling Patterns

1. **Custom Error Types**
```typescript
/**
 * Define domain-specific error types:
 * - Business logic errors
 * - Validation errors
 * - System errors
 * Include: Error codes, messages, recovery hints
 */
class PaymentError extends Error {
    constructor(
        message: string,
        public readonly error_code: string,
        public readonly recovery_hint?: string
    ) {
        super(message);
        this.name = 'PaymentError';
    }
}

class ValidationError extends PaymentError {
    constructor(
        message: string,
        public readonly field_name: string
    ) {
        super(message, 'VALIDATION_ERROR', 'Please check your input and try again');
        this.name = 'ValidationError';
    }
}

class NetworkError extends PaymentError {
    constructor(
        message: string,
        public readonly retry_after?: number
    ) {
        super(message, 'NETWORK_ERROR', 'Please check your connection and try again');
        this.name = 'NetworkError';
    }
}
```

2. **Error Recovery Logic**
```typescript
/**
 * Implement error recovery strategies:
 * - Retry mechanisms
 * - Fallback options
 * - Compensation actions
 * - State recovery
 */
class ErrorHandler {
    async with_retry<T>(
        operation: () => Promise<T>,
        options: {
            max_retries: number;
            delay_ms: number;
            backoff_factor: number;
        }
    ): Promise<T> {
        let last_error: Error;
        
        for (let attempt = 1; attempt <= options.max_retries; attempt++) {
            try {
                return await operation();
            } catch (error) {
                last_error = error;
                if (!this.is_retriable_error(error) || attempt === options.max_retries) {
                    throw error;
                }
                
                await this.delay(options.delay_ms * Math.pow(options.backoff_factor, attempt - 1));
            }
        }
        
        throw last_error;
    }
}
```

### Error Handling Best Practices

1. **Consistent Error Structure**
```typescript
/**
 * Define standard error response structure:
 * - Error identifier
 * - Human-readable message
 * - Technical details (dev mode)
 * - Recovery suggestions
 */
interface ErrorResponse {
    error_code: string;
    message: string;
    details?: {
        technical_info?: string;
        stack_trace?: string;
    };
    recovery_hint?: string;
    timestamp: string;
}
```

2. **Contextual Error Handling**
```typescript
/**
 * Handle errors based on context:
 * - User-facing errors
 * - System errors
 * - Integration errors
 * - Security errors
 */
class ContextualErrorHandler {
    handle_error(error: Error, context: {
        user_facing: boolean;
        severity: 'low' | 'medium' | 'high';
        component: string;
    }): ErrorResponse {
        // Implementation with appropriate handling based on context
    }
}
```

### Error Prevention Patterns

1. **Input Validation**
```typescript
/**
 * Implement comprehensive validation:
 * - Type checking
 * - Format validation
 * - Business rule validation
 * - Cross-field validation
 */
class InputValidator {
    validate<T>(data: T, schema: ValidationSchema): ValidationResult {
        // Implementation for input validation
    }
}
```

2. **Preconditions and Invariants**
```typescript
/**
 * Enforce system invariants:
 * - State validation
 * - Parameter checking
 * - Business rules
 * - Security constraints
 */
class ContractEnforcer {
    check_preconditions(conditions: Condition[]): void {
        // Implementation for precondition checking
    }
}
```

### Logging and Monitoring

1. **Error Logging Pattern**
```typescript
/**
 * Implement structured error logging:
 * - Error context
 * - System state
 * - User context
 * - Recovery actions
 */
interface ErrorLog {
    error: {
        type: string;
        message: string;
        stack?: string;
    };
    context: {
        user_id?: string;
        session_id?: string;
        component: string;
    };
    system_state: {
        memory_usage: number;
        cpu_usage: number;
        active_connections: number;
    };
    timestamp: string;
}
```

2. **Error Monitoring**
```typescript
/**
 * Monitor error patterns:
 * - Error frequency
 * - Impact severity
 * - Recovery success
 * - System health
 */
class ErrorMonitor {
    track_error(error: Error, context: ErrorContext): void {
        // Implementation for error tracking
    }
}
```

### Error Communication

1. **User Notifications**
```typescript
/**
 * Communicate errors to users:
 * - Clear messages
 * - Recovery steps
 * - Progress updates
 * - Support options
 */
class UserErrorNotifier {
    notify(error: Error, user_context: UserContext): UserNotification {
        // Implementation for user notifications
    }
}
```

2. **System Alerts**
```typescript
/**
 * Alert system stakeholders:
 * - Critical errors
 * - System outages
 * - Security incidents
 * - Performance issues
 */
class SystemAlerter {
    alert(error: Error, severity: AlertSeverity): void {
        // Implementation for system alerts
    }
}
```

### Anti-patterns to Avoid

1. **Error Handling**
   - Catching all errors blindly
   - Swallowing errors
   - Missing error context
   - Inconsistent error formats

2. **Error Recovery**
   - Infinite retry loops
   - Missing timeout handling
   - Unclear error states
   - Incomplete rollback

### Testing Error Handling

1. **Error Scenario Testing**
```typescript
/**
 * Test error handling paths:
 * - Expected errors
 * - Unexpected errors
 * - Recovery paths
 * - System resilience
 */
describe('Error Handling', () => {
    test('should handle network errors with retry', async () => {
        // Test implementation
    });
});
```

2. **Chaos Testing**
```typescript
/**
 * Test system resilience:
 * - Service failures
 * - Network issues
 * - Resource exhaustion
 * - Concurrent errors
 */
class ChaosTest {
    simulate_failure(scenario: FailureScenario): Promise<TestResult> {
        // Implementation for chaos testing
    }
}
```