# API Reference - {{PROJECT_NAME}}

**Version:** {{API_VERSION}}
**Base URL:** {{BASE_URL}}

**Last Updated:** {{DATE}}

## Table of Contents

- [Authentication](#authentication)
- [Common Headers](#common-headers)
- [Response Format](#response-format)
- [Errors](#errors)
- [Endpoints](#endpoints)
- [Rate Limiting](#rate-limiting)

## Authentication

### Authentication Method

{{AUTH_METHOD_DESCRIPTION}}

### Getting an API Key

{{GET_API_KEY_STEPS}}

### Using the API Key

```bash
curl -H "Authorization: Bearer YOUR_API_KEY" \
  {{BASE_URL}}/endpoint
```

### Token Refresh

{{TOKEN_REFRESH_INSTRUCTIONS}}

## Common Headers

### Required Headers

```http
{{REQUIRED_HEADERS}}
```

### Optional Headers

```http
{{OPTIONAL_HEADERS}}
```

## Response Format

### Success Response

```json
{
  "data": {{DATA}},
  "meta": {
    "page": {{PAGE}},
    "per_page": {{PER_PAGE}},
    "total": {{TOTAL}}
  }
}
```

### Error Response

```json
{
  "error": {
    "code": "{{ERROR_CODE}}",
    "message": "{{MESSAGE}}",
    "details": {{DETAILS}}
  }
}
```

## Errors

### Error Codes

| Code | HTTP Status | Description |
|------|-------------|-------------|
| {{CODE_1}} | {{STATUS_1}} | {{DESC_1}} |
| {{CODE_2}} | {{STATUS_2}} | {{DESC_2}} |
| {{CODE_3}} | {{STATUS_3}} | {{DESC_3}} |

### Common Errors

#### {{ERROR_NAME}}

**Status:** {{STATUS}}

**Description:** {{DESCRIPTION}}

**Solution:** {{SOLUTION}}

## Endpoints

### {{RESOURCE_NAME}}

#### GET {{ENDPOINT_PATH}}

**Description:** {{DESCRIPTION}}

**Authentication:** {{REQUIRED}}

**Query Parameters:**

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| {{PARAM_1}} | {{TYPE}} | {{REQ}} | {{DEFAULT}} | {{DESC}} |

**Request Example:**
```bash
curl {{BASE_URL}}{{ENDPOINT_PATH}}?{{PARAM_1}}={{VALUE}}
```

**Response (200 OK):**
```json
{{RESPONSE_EXAMPLE}}
```

#### POST {{ENDPOINT_PATH}}

**Description:** {{DESCRIPTION}}

**Request Body:**
```json
{
  {{REQUEST_BODY}}
}
```

**Validation:**
- {{VALIDATION_1}}
- {{VALIDATION_2}}

**Response (201 Created):**
```json
{{RESPONSE_EXAMPLE}}
```

#### PUT {{ENDPOINT_PATH}}/{{ID}}

**Description:** {{DESCRIPTION}}

**Request Body:** Same as POST

**Response (200 OK):**
```json
{{RESPONSE_EXAMPLE}}
```

#### DELETE {{ENDPOINT_PATH}}/{{ID}}

**Description:** {{DESCRIPTION}}

**Response:** 204 No Content

### {{OTHER_RESOURCES}}

{{REPEAT_FOR_EACH_RESOURCE}}

## Rate Limiting

### Limits

- **Authenticated:** {{AUTH_LIMIT}}
- **Unauthenticated:** {{UNAUTH_LIMIT}}
- **Burst:** {{BURST_LIMIT}}

### Headers

Rate limit headers are included in every response:

```http
X-RateLimit-Limit: 100
X-RateLimit-Remaining: 99
X-RateLimit-Reset: 1635724800
```

### Retry Strategy

{{RETRY_INSTRUCTIONS}}

## SDKs and Libraries

### Official SDKs

- **JavaScript:** {{SDK_LINK}}
- **Python:** {{SDK_LINK}}
- **Go:** {{SDK_LINK}}

### Community Libraries

- **Ruby:** {{LIBRARY_LINK}}
- **PHP:** {{LIBRARY_LINK}}

## Examples

### Complete Workflow

```javascript
{{COMPLETE_EXAMPLE}}
```

### Webhooks

{{WEBHOOK_DOCUMENTATION}}

---

*For architecture details, see [ARCHITECTURE.md](ARCHITECTURE.md)*
*For development guide, see [DEVELOPMENT.md](DEVELOPMENT.md)*
