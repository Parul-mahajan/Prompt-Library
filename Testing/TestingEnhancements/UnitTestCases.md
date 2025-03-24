# Unit Test Cases with GitHub Copilot

## Prompt 1: Basic Unit Test Generation
```
Use Case: To help developers create unit tests for their code using GitHub Copilot.

Prompt: You have a function/method that needs unit tests. The function details are as follows:

programming_language: {programming_language}
function_name: {function_name}
function_purpose: {function_purpose}
implementation: {implementation}

Generate unit tests for the function focusing on:
- Basic test cases covering typical scenarios
- Edge cases and boundary conditions
- Error handling tests
- Clear test names and documentation

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