# Identifying Potential Bugs

## Prompt 1: Code Review for Bug Prevention
```
Intent: To help developers identify potential bugs during code reviews.

Context: You are reviewing code for potential bugs. The code details are as follows:

Code_snippet: {code_snippet}
Programming_language: {programming_language}

Generate a list of potential bugs or issues, including:
- Logic errors.
- Edge cases.
- Error handling concerns.

Example:
Code_snippet:
```python
def divide(a, b):
    return a / b

result = divide(10, user_input)
```
Programming_language: "Python"
Potential Issues:
1. No validation for `b` being zero, which would cause a divide-by-zero error.
2. No type checking for `a` and `b`, which could cause issues if non-numeric values are passed.
3. No error handling (try-except) to gracefully handle exceptions.
4. The `user_input` variable is not defined before use.
```