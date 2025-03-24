# Writing API Documentation with GitHub Copilot

## Prompt 1: Generating Comprehensive API Documentation
```
Intent: To help developers create clear, comprehensive API documentation for endpoints using GitHub Copilot.

Context: You need to document an API endpoint. The endpoint details are as follows:

endpoint_name: {endpoint_name}
http_method: {http_method}
endpoint_url: {endpoint_url}
description: {description}
request_parameters: {request_parameters}
response_structure: {response_structure}
authentication_required: {authentication_required}
error_responses: {error_responses}

Generate comprehensive API documentation including:
- Endpoint overview
- Request format with example
- Response format with example
- Error codes and handling
- Usage notes/limitations

Example:
endpoint_name: "Get User Profile"
http_method: "GET"
endpoint_url: "/api/v1/users/{user_id}"
description: "Retrieves detailed profile information for a specified user"
request_parameters: [
  {
    "name": "user_id",
    "type": "string",
    "required": true,
    "description": "Unique identifier for the user"
  },
  {
    "name": "include_activity",
    "type": "boolean",
    "required": false,
    "description": "Whether to include recent user activity in response",
    "default": false
  }
]
response_structure: {
  "user_id": "string",
  "username": "string",
  "email": "string",
  "profile_image": "string (URL)",
  "account_type": "string (enum: basic, premium, admin)",
  "created_at": "string (ISO date)",
  "last_login": "string (ISO date)",
  "activity_feed": "array (only if include_activity=true)"
}
authentication_required: true
error_responses: [
  {
    "status_code": 401,
    "message": "Unauthorized access",
    "description": "Authentication credentials missing or invalid"
  },
  {
    "status_code": 404,
    "message": "User not found",
    "description": "No user exists with the specified user_id"
  }
]

## Get User Profile

Retrieves detailed profile information for a specified user.

### Endpoint

```
GET /api/v1/users/{user_id}
```

### Authentication

**Required**: API key must be provided in the request header.

```
Authorization: Bearer {api_key}
```

### Request Parameters

#### Path Parameters

| Parameter | Type   | Required | Description               |
|-----------|--------|----------|---------------------------|
| user_id   | string | Yes      | Unique identifier for the user |

#### Query Parameters

| Parameter        | Type    | Required | Default | Description                                     |
|------------------|---------|----------|---------|-------------------------------------------------|
| include_activity | boolean | No       | false   | Whether to include recent user activity in response |

### Example Request

```bash
curl -X GET \
  'https://api.example.com/api/v1/users/usr_12345?include_activity=true' \
  -H 'Authorization: Bearer your_api_key_here'
```

### Response Format

A successful response returns HTTP status code `200 OK` and a JSON object with the following structure:

```json
{
  "user_id": "usr_12345",
  "username": "johndoe",
  "email": "john.doe@example.com",
  "profile_image": "https://api.example.com/images/profiles/johndoe.jpg",
  "account_type": "premium",
  "created_at": "2023-01-15T08:30:00Z",
  "last_login": "2023-05-20T14:22:10Z",
  "activity_feed": [
    {
      "action": "login",
      "timestamp": "2023-05-20T14:22:10Z",
      "ip_address": "192.168.1.1"
    },
    {
      "action": "profile_update",
      "timestamp": "2023-05-18T09:45:22Z",
      "ip_address": "192.168.1.1"
    }
  ]
}
```

> Note: The `activity_feed` array is only included when `include_activity=true` is specified in the request.

### Error Responses

| Status Code | Message | Description |
|-------------|---------|-------------|
| 401 | Unauthorized access | Authentication credentials missing or invalid |
| 404 | User not found | No user exists with the specified user_id |

### Usage Notes

1. Rate limiting: This endpoint is limited to 100 requests per minute per API key.
2. The `profile_image` URL is valid for 24 hours. Do not cache this URL for longer periods.
3. For privacy reasons, email addresses are only provided for users who have enabled public email sharing.
```