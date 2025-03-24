# Suggesting Improvements

## Prompt 1: Code Improvement Recommendations
```
Intent: To help developers suggest improvements during code reviews.

Context: You are reviewing code and suggesting improvements. The code details are as follows:

Code_snippet: {code_snippet}
Programming_language: {programming_language}

Generate a list of improvement suggestions, including:
- Code readability enhancements.
- Performance optimizations.
- Best practices implementation.

Example:
Code_snippet:
```javascript
function getUsers() {
  var data = [];
  for(var i=0; i<users.length; i++) {
    if(users[i].active == true) {
      data.push(users[i]);
    }
  }
  return data;
}
```
Programming_language: "JavaScript"
Improvement Suggestions:
1. Use `const` or `let` instead of `var` for better scoping.
2. Use filter method for cleaner code: `return users.filter(user => user.active);`
3. Simplify the condition to `if(users[i].active)` as `== true` is redundant.
4. Add JSDoc comments to document the function's purpose and parameters.
```