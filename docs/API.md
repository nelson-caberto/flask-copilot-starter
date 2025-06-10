# API Documentation

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

### Using curl
```bash
# Health check
curl -X GET http://localhost:5000/api/health
```

### Using Python requests
```python
import requests

response = requests.get('http://localhost:5000/api/health')
print(response.json())
```

---
*Last updated: [Current Date]*
*Version: [Current Version]*
