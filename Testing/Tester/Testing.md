# Tester - Testing Stage

## Prompt 1: Automation Test Cases
```
You are a tester responsible for creating automation test cases for the following feature:

Feature Name: {feature_name}
Test Scenarios: {test_scenarios}

Generate a table of test cases in the following format:
- Test Case ID
- Test Scenario
- Steps to Execute
- Expected Result
- Actual Result (to be filled later)
- Status (Pass/Fail, to be filled later)
```

## Prompt 2: Manual Test Cases
```
You are a tester creating manual test cases for a feature. Use the following details:

Feature Name: {feature_name}
Test Scenarios: {test_scenarios}

Generate a list of manual test cases with detailed steps and expected results.
```

## Prompt 3: Creating Comprehensive Test Scenarios
```
Intent: To help testers create comprehensive test scenarios for a feature.

Context: You are testing a feature with the following details:

Feature Name: {feature_name}
Requirements: {requirements}

Generate a list of test scenarios, ensuring:
- Coverage of functional and non-functional requirements.
- Inclusion of edge cases and negative scenarios.
- Alignment with user expectations.

Example:
Test Scenario: Verify login functionality with valid credentials.
Steps:
1. Navigate to the login page.
2. Enter valid username and password.
3. Click the login button.
Expected Result: User is redirected to the dashboard.
```