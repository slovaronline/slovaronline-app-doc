# SLOVARonline API Documentation (v1-alpha)

## Overview

This API allows users to search for phrases and retrieve detailed information about specific phrases from the `*.slovaronline.com` domains. 
The API uses an API key for authentication, which should be provided in the query string for each request.

### Base URL
```
https://*.slovaronline.com/api/v1-alpha/
```
The full list of available domain: [https://slovaronline.com/dictionaries](https://slovaronline.com/dictionaries). 

## Endpoints

### 1. Search for Phrases

**Endpoint**: `/api/v1-alpha/search`

**Method**: `GET`

**Description**: This endpoint allows users to search for phrases that match the query string (`q`).

**Request Parameters**:
- `q` (required): The query string (e.g., part of the phrase or word to search). Use it for `autocomplete` functionality. 
- `api_key` (required): The API key for authentication.

**Example Request**:
```
GET https://*.slovaronline.com/api/v1-alpha/search?q=back&api_key=YOUR_API_KEY
```

**Response**:
```json
{
  "result": {
    "phrases": ["backboard", "backcourt", "backdoor", ...]
  },
  "status": "ok"
}
```

**Error Handling**:
If the `q` or `api_key` parameter is missing or invalid:
```json
{
  "error": "Invalid request, missing required parameters",
  "status": "error"
}
```

---

### 2. Get Phrase Description

**Endpoint**: `/api/v1-alpha/phrase`

**Method**: `GET`

**Description**: Retrieves the full description of a specific phrase based on the query string (`q`).

**Request Parameters**:
- `q` (required): The specific phrase to retrieve the description for.
- `api_key` (required): The API key for authentication.

**Example Request**:
```
GET https://*.slovaronline.com/api/v1-alpha/phrase?q=backdoor&api_key=YOUR_API_KEY
```

**Response**:
```json
{
  "result": [
    {
      "phrase": "backdoor",
      "full": "https://*.slovaronline.com/337-backdoor",
      "description": "за спиной у соперника, букв. `через заднюю дверь`"
    }
  ],
  "status": "ok"
}
```

**Error Handling**:
If the `q` or `api_key` is missing or invalid:
```json
{
  "error": "Invalid request, missing required parameters",
  "status": "error"
}
```

---

## Authentication

### API Key in Query String

Both endpoints require the API key to be passed in the query string:

- **Search Request**:
```
GET /api/v1-alpha/search?q=QUERY&api_key=YOUR_API_KEY
```

- **Phrase Description Request**:
```
GET /api/v1-alpha/phrase?q=QUERY&api_key=YOUR_API_KEY
```

## Error Responses

- **400 Bad Request**: If the request is missing required parameters or is malformed.
```json
{
  "error": "Invalid request, missing required parameters",
  "status": "error"
}
```

- **403 Unauthorized**: If the API key is invalid or missing.
```json
{
  "error": "Unauthorized, invalid API key",
  "status": "error"
}
```

- **404 Not Found**: If the requested resource (phrase) cannot be found.
```json
{
  "error": "Resource not found",
  "status": "error"
}
```

---

### Terms and conditions
API is provides as is and no future support is guaranteed. Additional terms are located [here](https://slovaronline.com/terms_of_use).

### Contact

For support or questions about the API, please contact [connect@slovaronline.com](mailto:connect@slovaronline.com).
