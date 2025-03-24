# Secure Configurations for GitHub Copilot

## Prompt 1: Creating Basic Secure Configuration Templates
```
Intent: To help developers create secure configuration files using GitHub Copilot.

Context: You are setting up security configurations for an application. The application details are as follows:

application_type: {application_type}
environment: {environment}

Generate a basic secure configuration template, including:
- Standard security headers
- Basic authentication settings
- Common security patterns

Example:
application_type: "Web Application"
environment: "Production"

Secure Configuration Template:
```yaml
# Basic web application security configuration

# Server security headers
security_headers:
  # Prevent clickjacking attacks
  x_frame_options: DENY
  
  # Prevent MIME type sniffing
  x_content_type_options: nosniff
  
  # Enable XSS protection in browsers
  x_xss_protection: "1; mode=block"
  
  # Content Security Policy
  content_security_policy: "default-src 'self'; script-src 'self'; object-src 'none'; img-src 'self' data:;"

# Cookie settings
cookies:
  secure: true
  http_only: true
  same_site: strict
  
# Authentication settings
authentication:
  # Minimum password requirements
  password_min_length: 12
  password_require_lowercase: true
  password_require_uppercase: true
  password_require_digits: true
  password_require_special_chars: true
  
  # Session management
  session_timeout_minutes: 30
  max_login_attempts: 5
  lockout_duration_minutes: 15
  
# CORS configuration
cors:
  allowed_origins:
    - https://example.com
  allowed_methods:
    - GET
    - POST
  allowed_headers:
    - Content-Type
    - Authorization
  expose_headers:
    - X-Request-ID
  max_age_seconds: 86400

# Logging (avoid sensitive data)
logging:
  level: INFO
  exclude_fields:
    - password
    - token
    - credit_card
```

Key points to consider:
1. Use standard security headers and settings
2. Focus on common security patterns rather than complex implementations
3. Provide templates that are easy to customize
4. Include basic security concepts applicable to most applications
```