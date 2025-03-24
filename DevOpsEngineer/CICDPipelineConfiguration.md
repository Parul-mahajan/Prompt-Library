# DevOps CI/CD Pipeline Configuration

## Prompt 1: Creating Basic CI Pipeline Configuration
```
Intent: To help developers create CI pipeline configuration files using GitHub Copilot.

Context: You are setting up a Continuous Integration pipeline for a project. The project details are as follows:

project_type: {project_type}
programming_language: {programming_language}
testing_framework: {testing_framework}

Generate a CI pipeline configuration file for GitHub Actions, including:
- Basic setup and triggers
- Dependencies installation
- Testing configuration
- Simple reporting

Example:
project_type: "Web Application"
programming_language: "JavaScript (Node.js)"
testing_framework: "Jest"

CI Pipeline Configuration:
```yaml
name: Node.js CI Pipeline

on:
  push:
    branches: [ main, develop ]
  pull_request:
    branches: [ main, develop ]

jobs:
  build_and_test:
    runs-on: ubuntu-latest
    
    strategy:
      matrix:
        node-version: [14.x, 16.x]
    
    steps:
    - uses: actions/checkout@v2
    
    - name: Setup Node.js ${{ matrix.node-version }}
      uses: actions/setup-node@v2
      with:
        node-version: ${{ matrix.node-version }}
        cache: 'npm'
    
    - name: Install dependencies
      run: npm ci
    
    - name: Lint code
      run: npm run lint
    
    - name: Run tests
      run: npm test
    
    - name: Build project
      run: npm run build
    
    - name: Upload test results
      uses: actions/upload-artifact@v2
      with:
        name: test-results
        path: coverage/
```

Key points to consider:
1. Use standard CI/CD services like GitHub Actions, GitLab CI, or Azure DevOps
2. Focus on commonly used configuration elements and syntax
3. Use simple triggers, dependencies, and test steps
4. Avoid complex conditions or custom script executions
```