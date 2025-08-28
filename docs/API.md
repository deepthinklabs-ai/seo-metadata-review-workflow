# API Documentation

## Webhook Endpoint

### POST /seo-metadata-review

Analyzes SEO metadata for a given URL.

#### Request Body

```json
{
  "url": "https://example.com"
}
```

#### Response

```json
{
  "url": "https://example.com",
  "metadata": {
    "title": "Example Website",
    "description": "This is an example website",
    "ogTitle": "Example Website - Open Graph",
    "ogDescription": "This is an example website for Open Graph"
  },
  "analysis": {
    "title": {
      "length": 15,
      "recommendations": []
    },
    "description": {
      "length": 26,
      "recommendations": ["Description too short (recommended: 120-160 characters)"]
    },
    "openGraph": {
      "recommendations": []
    },
    "overallScore": 85,
    "timestamp": "2025-08-28T08:14:58.000Z"
  }
}
```

#### Status Codes

- `200 OK`: Successfully analyzed URL
- `400 Bad Request`: Invalid request body or URL
- `404 Not Found`: URL not accessible
- `500 Internal Server Error`: Analysis failed

## Scoring System

The workflow provides an overall SEO score based on various factors:

### Title Tag (20 points penalty per issue)
- Missing title tag
- Title too short (< 30 characters)
- Title too long (> 60 characters)

### Meta Description (15 points penalty per issue)
- Missing meta description
- Description too short (< 120 characters)
- Description too long (> 160 characters)

### Open Graph (10 points penalty per issue)
- Missing og:title
- Missing og:description

### Score Calculation

Starting from 100 points, penalties are deducted based on the issues found.
Minimum score is 0.
