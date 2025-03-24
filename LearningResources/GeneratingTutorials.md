# Generating Tutorials

## Prompt 1: Creating Technical Tutorials
```
Intent: To help developers create tutorials for technical topics.

Context: You are creating a tutorial for a new technology. The details are as follows:

Technology_name: {technology_name}
Target_audience: {target_audience}

Generate a tutorial outline, including:
- Introduction to the technology.
- Step-by-step instructions.
- Code examples and explanations.

Example:
Technology_name: "React Hooks"
Target_audience: "Junior Frontend Developers"
Tutorial Outline:
1. Introduction to React Hooks
   - What are hooks and why were they introduced?
   - Advantages over class components.

2. Setting Up Your Environment
   - Requirements: Node.js, npm, create-react-app.
   - Step-by-step setup instructions.

3. Basic Hooks
   - useState: Managing component state.
   - useEffect: Handling side effects.
   - Code example: Creating a simple counter application.

4. Advanced Hooks
   - useContext: Managing global state.
   - useRef: Accessing DOM elements.
   - Custom hooks: Creating reusable hook logic.

5. Best Practices
   - When to use each hook.
   - Common pitfalls to avoid.
```