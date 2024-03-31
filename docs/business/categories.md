## Get Business Categories

### Request

**Method:** `GET`

**Path:** `/api/v1/app/business/categories`

**Authorization:**

Bearer token required.

**Parameters:** None

**Example Result:**

```json
{
    "success": true,
    "data": [
        "Agriculture",
        "Construction",
        "Education",
        "Finance",
        "Health Care",
        "Manufacturing",
        "Retail",
        "Services",
        "Technology",
        "Transportation"
    ]
}
```

**Status Code:** `200 OK`

**Description:** This endpoint retrieves a list of available business categories.
