# Identifying Security Vulnerabilities

## Prompt 1: Security Code Review
```
Intent: To help developers identify security vulnerabilities in their code.

Context: You are conducting a security review of code. The code details are as follows:

Code_snippet: {code_snippet}
Programming_language: {programming_language}
Application_type: {application_type}

Generate a list of potential security vulnerabilities, including:
- Injection vulnerabilities.
- Authentication issues.
- Data exposure risks.

Example:
Code_snippet:
```php
$username = $_POST['username'];
$password = $_POST['password'];
$query = "SELECT * FROM users WHERE username='$username' AND password='$password'";
$result = mysqli_query($connection, $query);
if(mysqli_num_rows($result) > 0) {
    $_SESSION['user'] = $username;
    echo "Login successful";
}
```
Programming_language: "PHP"
Application_type: "Web Application"

Security Vulnerabilities:
1. SQL Injection: The code directly inserts user input into the SQL query without sanitization.
2. Plain Text Passwords: Passwords are stored and compared in plain text rather than being hashed.
3. Insufficient Authentication: No account lockout mechanism for failed login attempts.
4. Session Fixation: The session is not regenerated after successful login.
5. Information Disclosure: Error messages may reveal sensitive information about the database structure.

Recommendations:
1. Use prepared statements or parameterized queries to prevent SQL injection.
2. Hash passwords using a strong algorithm like bcrypt.
3. Implement account lockout after multiple failed attempts.
4. Regenerate session IDs after login with session_regenerate_id().
5. Use generic error messages that don't reveal system details.
```