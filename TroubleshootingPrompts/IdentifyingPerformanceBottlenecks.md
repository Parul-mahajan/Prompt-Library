# Identifying Performance Bottlenecks

## Prompt 1: Analyzing Performance Issues
```
Use Case: To help developers identify performance bottlenecks in their code.

Prompt: You are diagnosing performance issues in an application. The application details are as follows:

Application_name: {application_name}
Performance_metrics: {performance_metrics}

Generate a step-by-step plan to identify performance bottlenecks, including:
- Analyzing the performance metrics.
- Identifying critical sections of code.
- Suggesting profiling techniques.

Example:
Application_name: "E-commerce Website"
Performance_metrics: "Page load time: 5s, Database query time: 3s"
Plan:
1. Analyze the database queries that are taking the most time.
2. Check for N+1 query issues.
3. Identify if caching can be implemented for frequently accessed data.
```