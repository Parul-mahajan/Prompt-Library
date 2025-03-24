# Unit Test Cases with GitHub Copilot

## Prompt 1: Basic Unit Test Generation
```
Intent: To help developers create unit tests for their code using GitHub Copilot.

Context: You have a function/method that needs unit tests. The function details are as follows:

programming_language: {programming_language}
function_name: {function_name}
function_purpose: {function_purpose}
implementation: {implementation}

Generate unit tests for the function focusing on:
- Basic test cases covering typical scenarios
- Edge cases and boundary conditions
- Error handling tests
- Clear test names and documentation

Example:
programming_language: "TypeScript"
function_name: "calculateDiscount"
function_purpose: "Calculates discount amount based on purchase total and customer type"
implementation: 
```typescript
/**
 * Calculates the discount amount based on purchase total and customer type.
 * @param purchase_total The total purchase amount
 * @param customer_type The type of customer ('regular', 'premium', or 'vip')
 * @returns The discount amount
 * @throws Error if inputs are invalid
 */
function calculateDiscount(purchase_total: number, customer_type: string): number {
  // Validate inputs
  if (purchase_total < 0) {
    throw new Error('Purchase total cannot be negative');
  }
  
  if (!['regular', 'premium', 'vip'].includes(customer_type)) {
    throw new Error('Invalid customer type');
  }
  
  // Calculate base discount based on purchase total
  let discount_rate = 0;
  if (purchase_total >= 100 && purchase_total < 500) {
    discount_rate = 0.05; // 5% discount
  } else if (purchase_total >= 500 && purchase_total < 1000) {
    discount_rate = 0.1; // 10% discount
  } else if (purchase_total >= 1000) {
    discount_rate = 0.15; // 15% discount
  }
  
  // Apply customer type modifier
  if (customer_type === 'premium') {
    discount_rate += 0.05; // Additional 5% for premium customers
  } else if (customer_type === 'vip') {
    discount_rate += 0.1; // Additional 10% for VIP customers
  }
  
  // Calculate and return discount amount
  return purchase_total * discount_rate;
}
```

Unit Tests:
```typescript
import { expect } from 'chai';
import { describe, it } from 'mocha';

describe('calculateDiscount', () => {
  // Test typical scenarios
  it('should return zero discount for purchases under $100 with regular customer', () => {
    const result = calculateDiscount(50, 'regular');
    expect(result).to.equal(0);
  });
  
  it('should apply 5% discount for purchases between $100-$499 with regular customer', () => {
    const result = calculateDiscount(200, 'regular');
    expect(result).to.equal(10); // $200 * 0.05 = $10
  });
  
  it('should apply 10% discount for purchases between $500-$999 with regular customer', () => {
    const result = calculateDiscount(600, 'regular');
    expect(result).to.equal(60); // $600 * 0.1 = $60
  });
  
  it('should apply 15% discount for purchases over $1000 with regular customer', () => {
    const result = calculateDiscount(2000, 'regular');
    expect(result).to.equal(300); // $2000 * 0.15 = $300
  });
  
  // Test customer type modifiers
  it('should add 5% to discount rate for premium customers', () => {
    const regularDiscount = calculateDiscount(200, 'regular');
    const premiumDiscount = calculateDiscount(200, 'premium');
    
    expect(regularDiscount).to.equal(10); // $200 * 0.05 = $10
    expect(premiumDiscount).to.equal(20); // $200 * (0.05 + 0.05) = $20
  });
  
  it('should add 10% to discount rate for VIP customers', () => {
    const regularDiscount = calculateDiscount(200, 'regular');
    const vipDiscount = calculateDiscount(200, 'vip');
    
    expect(regularDiscount).to.equal(10); // $200 * 0.05 = $10
    expect(vipDiscount).to.equal(30); // $200 * (0.05 + 0.1) = $30
  });
  
  // Test boundary conditions
  it('should handle exactly $100 purchase correctly', () => {
    const result = calculateDiscount(100, 'regular');
    expect(result).to.equal(5); // $100 * 0.05 = $5
  });
  
  it('should handle exactly $500 purchase correctly', () => {
    const result = calculateDiscount(500, 'regular');
    expect(result).to.equal(50); // $500 * 0.1 = $50
  });
  
  it('should handle exactly $1000 purchase correctly', () => {
    const result = calculateDiscount(1000, 'regular');
    expect(result).to.equal(150); // $1000 * 0.15 = $150
  });
  
  it('should handle zero purchase amount correctly', () => {
    const result = calculateDiscount(0, 'regular');
    expect(result).to.equal(0);
  });
  
  // Test error handling
  it('should throw error for negative purchase amount', () => {
    expect(() => calculateDiscount(-10, 'regular')).to.throw('Purchase total cannot be negative');
  });
  
  it('should throw error for invalid customer type', () => {
    expect(() => calculateDiscount(100, 'unknown')).to.throw('Invalid customer type');
  });
});
```

Key points to consider:
1. Use standard testing frameworks for the language
2. Test both normal and edge cases
3. Group tests logically by behavior or feature
4. Use descriptive test names that explain what's being tested
5. Include assertions that verify the correct behavior
6. Verify error handling for invalid inputs
```

## Prompt 2: Testing Patterns with GitHub Copilot

### Testing Strategy Template
```markdown
Intent: To help developers create comprehensive testing strategies using GitHub Copilot.

Context: You are developing a testing strategy for a component. Provide:
- Testing pyramid structure
- Test categorization
- Coverage goals
- Automation approach

Example:
component_type: "REST API Service"
test_requirements: {
  "unit_coverage": "90%",
  "integration_coverage": "80%",
  "e2e_coverage": "critical paths"
}
```

### Testing Patterns Implementation

1. **Unit Test Pattern**
```typescript
/**
 * Component: User Authentication Service
 * Test Category: Unit Tests
 * Coverage Goals: 
 * - Input validation
 * - Business logic
 * - Error handling
 */
describe('UserAuthService', () => {
    // Setup and teardown
    beforeEach(() => {
        // Initialize test dependencies
    });

    describe('validateCredentials', () => {
        test('should validate correct credentials', async () => {
            // Test implementation
        });

        test('should handle invalid credentials', async () => {
            // Test implementation
        });

        test('should handle edge cases', async () => {
            // Test implementation
        });
    });
});
```

2. **Integration Test Pattern**
```typescript
/**
 * Feature: User Registration Flow
 * Test Category: Integration Tests
 * Coverage: 
 * - Database operations
 * - Email service integration
 * - Error scenarios
 */
describe('UserRegistrationFlow', () => {
    // Setup and teardown
    beforeAll(async () => {
        // Initialize test database
        // Start mock services
    });

    afterAll(async () => {
        // Cleanup test data
        // Stop mock services
    });

    test('should complete registration process', async () => {
        // Test implementation
    });
});
```

### Best Practices for AI-Assisted Testing

1. **Test Generation Guidance**
   - Provide clear context and requirements
   - Include edge cases and error scenarios
   - Specify testing framework preferences
   - Define assertion patterns

2. **Coverage Strategy**
   ```markdown
   Define coverage goals for:
   - Functions and methods
   - Branches and conditions
   - Integration points
   - Error handling paths
   ```

3. **Maintenance Approach**
   - Keep tests focused and atomic
   - Use descriptive test names
   - Document test intentions
   - Update tests with code changes

### Test Data Management

1. **Test Data Generation**
```typescript
/**
 * Guide Copilot to generate test data with:
 * - Realistic data patterns
 * - Edge case values
 * - Invalid input scenarios
 * - Different data types
 */
const test_data_examples = [
    {
        scenario: "valid_user",
        input: {
            user_name: "john_doe",
            email: "john@example.com",
            age: 30
        },
        expected: "success"
    },
    {
        scenario: "invalid_email",
        input: {
            user_name: "john_doe",
            email: "invalid-email",
            age: 30
        },
        expected: "validation_error"
    }
];
```

2. **Mock Data Patterns**
```typescript
/**
 * Guide Copilot to generate mocks with:
 * - Common service responses
 * - Error conditions
 * - Timing variations
 * - Network states
 */
const mock_patterns = {
    success_response: {
        status: 200,
        body: { /* success data */ }
    },
    error_response: {
        status: 400,
        error: { /* error details */ }
    }
};
```

### Automated Verification Patterns

1. **State Verification**
```typescript
/**
 * Verify:
 * - Initial state
 * - State transitions
 * - Final state
 * - Side effects
 */
expect(result).toMatchObject({
    status: 'success',
    data: expect.any(Object),
    timestamp: expect.any(Number)
});
```

2. **Behavior Verification**
```typescript
/**
 * Verify:
 * - Function calls
 * - Call order
 * - Parameters
 * - Return values
 */
expect(mockService.method).toHaveBeenCalledWith(
    expect.objectContaining({
        id: expect.any(String),
        timestamp: expect.any(Number)
    })
);
```

### Testing Anti-patterns to Avoid

1. **Test Structure**
   - Avoid testing implementation details
   - Don't create brittle tests
   - Prevent test interdependence
   - Skip redundant test cases

2. **Test Maintenance**
   - Don't duplicate test code
   - Avoid hardcoded test data
   - Don't ignore failed tests
   - Keep tests focused and clear