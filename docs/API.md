# API Documentation

## Project Types
This documentation covers API patterns for both:
- **Flask Applications**: Complete web applications with their own APIs
- **Flask Extensions**: Extensions that may provide API endpoints or modify existing APIs

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

### Standard Error Format
```json
{
  "error": "Error message",
  "code": "ERROR_CODE",
  "details": {}
}
```

### HTTP Status Codes
- `200` - Success
- `400` - Bad Request
- `401` - Unauthorized
- `403` - Forbidden
- `404` - Not Found
- `500` - Internal Server Error

## Rate Limiting
[Document rate limiting when implemented]

## Examples

### Flask Application APIs

#### Using curl
```bash
# Health check
curl -X GET http://localhost:5000/api/health
```

#### Using Python requests
```python
import requests

response = requests.get('http://localhost:5000/api/health')
print(response.json())
```

### Flask Extension APIs

#### Extension with API endpoints
```python
from flask import Flask
from your_extension import YourExtension

app = Flask(__name__)
extension = YourExtension()
extension.init_app(app)

# Extension may add its own routes like /api/extension/status
```

#### Testing Extension APIs
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
```

---
*Last updated: June 11, 2025*
*Update this documentation whenever API endpoints are added, modified, or removed.*
