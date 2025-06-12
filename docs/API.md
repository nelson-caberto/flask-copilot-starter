# API Documentation ⚡

> **SPEED-FIRST API DEVELOPMENT** | Focus: Immediate Implementation | No Over-Engineering

## ⚡ **AI Setup**: Say `reload_context.md` for instant project context

## ⚡ Quick API Testing
```bash
# IMMEDIATE HEALTH CHECK - NO SETUP REQUIRED
curl -X GET http://localhost:5000/api/health
```

## Project Types
This documentation covers API patterns for both:
- **Flask Applications**: Complete web applications with their own APIs
- **Flask Extensions**: Extensions that may provide API endpoints or modify existing APIs

## ⚡ API Development Rules (Anti-Paralysis)

### IMMEDIATE Decision Hierarchy
1. **REST conventions** (80% default) - Use standard HTTP methods
2. **Existing patterns** (15%) - Follow current endpoint structure  
3. **Custom approach** (5% only) - When standards insufficient

### NO-ANALYSIS API Operations
**Auto-proceed rules** - These require ZERO analysis:
- CRUD endpoints → Use REST conventions immediately
- JSON responses → Use standard format below
- Error handling → Use standard error format below
- Authentication → Use existing auth patterns

### EMERGENCY Protocol for API Design
**If stuck > 2 minutes on API decisions:**
1. ⏰ Use REST conventions immediately
2. 🎯 Return JSON with standard format
3. 🚀 Add proper error handling
4. 📖 Refer to existing endpoints as examples

## Base URL
- Development: `http://localhost:5000`
- Production: `https://your-domain.com`

## Authentication
[Document authentication methods when implemented]

## Endpoints

### Health Check
- **GET** `/api/health`
- **Description**: Check if the API is running
- **Authentication**: None required
- **Response**: 
  ```json
  {
    "status": "healthy",
    "message": "Flask Copilot Starter is running!"
  }
  ```

## Error Responses

## ⚡ Standard Response Formats (NO CUSTOMIZATION)

### Success Response ⚡
```json
{
  "status": "success",
  "data": { /* response data */ },
  "message": "Operation completed successfully"
}
```

### Error Response ⚡
```json
{
  "status": "error", 
  "error": "Error message",
  "code": "ERROR_CODE",
  "details": {}
}
```

### HTTP Status Codes ⚡ (USE THESE EXACTLY)
- `200` - Success
- `201` - Created  
- `400` - Bad Request
- `401` - Unauthorized
- `403` - Forbidden
- `404` - Not Found
- `422` - Validation Error
- `500` - Internal Server Error

## ⚡ Speed-First API Examples

### Flask Application APIs ⚡

#### IMMEDIATE Testing with curl
```bash
# Health check ⚡
curl -X GET http://localhost:5000/api/health

# POST example ⚡  
curl -X POST http://localhost:5000/api/users \
  -H "Content-Type: application/json" \
  -d '{"name": "John Doe", "email": "john@example.com"}'

# GET with parameters ⚡
curl -X GET "http://localhost:5000/api/users?page=1&limit=10"
```

#### IMMEDIATE Testing with Python
```python
import requests

# Health check ⚡
response = requests.get('http://localhost:5000/api/health')
print(response.json())

# POST example ⚡
data = {"name": "John Doe", "email": "john@example.com"}
response = requests.post('http://localhost:5000/api/users', json=data)
print(response.json())
```

### Flask Extension APIs ⚡

#### Extension with API endpoints (NO ANALYSIS)
```python
from flask import Flask
from your_extension import YourExtension

app = Flask(__name__)
extension = YourExtension()
extension.init_app(app)

# Extension adds routes like /api/extension/status (follow this pattern)
```

#### IMMEDIATE Extension API Testing
```python
import pytest
from flask import Flask
from your_extension import YourExtension

def test_extension_api():
    app = Flask(__name__)
    extension = YourExtension()
    extension.init_app(app)
    
    with app.test_client() as client:
        response = client.get('/api/extension/status')
        assert response.status_code == 200
        assert response.json['status'] == 'success'
```

## ⚡ API Development Anti-Paralysis Checklist

### Before Creating New Endpoint (< 2 minutes total)
- [ ] ⚡ Use REST conventions (GET, POST, PUT, DELETE)
- [ ] ⚡ Follow `/api/resource` naming pattern
- [ ] ⚡ Return standard JSON format
- [ ] ⚡ Add basic error handling

### After Creating Endpoint (< 5 minutes total)  
- [ ] ⚡ Test with curl command
- [ ] ⚡ Add to this documentation
- [ ] ⚡ Create basic test case
- [ ] ⚡ Update CHANGELOG.md

---
*Last updated: June 11, 2025 - Enhanced with speed-first API development patterns*
*Update this documentation whenever API endpoints are added, modified, or removed.*
