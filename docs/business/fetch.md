## Get Profile's Business

### Request

**Method:** `GET`

**Path:** `/api/v1/app/business/{profile}`

**Authorization:**

Bearer token required.

**Parameters:**

| Name       | Type     | Required | Description                 |
|------------|----------|----------|-----------------------------|
| `profile`  | `string` | Yes      | The user's phone number.   |

**Example Result:**

```json
{
    "success": true,
    "data": {
        "id": 1,
        "profile_phone": "263775123456",
        "business_name": "Acme Inc.",
        "business_category": "Technology",
        "bp_number": "BP123456",
        "home_address": {
            "id": 1,
            "address_line_1": "123 Main St",
            "address_line_2": "Apt 4B",
            "city": "Mutare"
        },
        "business_address": {
            "id": 2,
            "address_line_1": "456 Business Ave",
            "address_line_2": "Suite 200",
            "city": "Mutare"
        }
    }
}
```

**Status Code:** `200 OK`

**Errors:**

- `404 Not Found` - If the profile does not have a business associated with it.

**Description:** This endpoint retrieves the business and associated addresses for a given user profile.
