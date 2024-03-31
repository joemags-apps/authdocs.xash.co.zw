## Create Business for Profile

### Request

**Method:** `POST`

**Path:** `/api/v1/app/business/{profile}`

**Parameters:**

| Name                     | Type     | Required | Description                                     |
|--------------------------|----------|----------|--------------------------------------------------|
| `business_name`          | `string` | Yes      | The name of the business.                       |
| `business_category`      | `string` | Yes      | The category of the business.                   |
| `bp_number`              | `string` | Yes      | The business partner number.                    |
| `address_line_1`         | `string` | Yes      | The first line of the home address.             |
| `address_line_2`         | `string` | No       | The second line of the home address.            |
| `city`                   | `string` | Yes      | The city of the home address.                   |
| `business_address_line_1`| `string` | Yes      | The first line of the business address.         |
| `business_address_line_2`| `string` | No       | The second line of the business address.        |
| `business_city`          | `string` | Yes      | The city of the business address.               |

**Example Result:**

```json
{
    "success": true,
    "message": "Business created successfully.",
    "data": {
        "id": 1,
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

**Status Code:** `201 Created`

**Errors:**

- `400 Bad Request` - If the profile already has a business associated with it.
- `500 Internal Server Error` - If there was an issue creating the business or addresses in the database.

**Description:** This endpoint creates a new business and associated home and business addresses for a user profile.
