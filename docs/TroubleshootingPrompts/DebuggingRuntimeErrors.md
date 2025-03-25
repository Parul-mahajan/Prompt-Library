# Debugging Runtime Errors with GitHub Copilot

## Prompt 1: Troubleshooting Common Runtime Errors
```
Intent: To help developers debug runtime errors using GitHub Copilot.

Prompt:
  Youare debugging a runtime error in your code. The error details are as follows #error_type: {error_type}
  error_type: "TypeError"
execution_environment: {execution_environment}

Analyze the error and provide:
- Explanation of the error
- Potential causes
- Code fixes with clear explanations
- Prevention tips
```

## Prompt 2: Debugging Patterns with GitHub Copilot

### Debugging Strategy Template
```markdown
Intent: To guide systematic debugging using GitHub Copilot.

Prompt: You are debugging an issue in your code. Describe:
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