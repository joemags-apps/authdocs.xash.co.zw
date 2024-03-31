
## Update Business and Addresses

### Request

**Method:** `PATCH`

**Path:** `/api/v1/app/business/{business}`

**Parameters:**

| Name                     | Type     | Required | Description                                     |
|--------------------------|----------|----------|--------------------------------------------------|
| `business`               | `integer`| Yes      | The ID of the business to update.               |
| `business_name`          | `string` | No       | The updated name of the business.               |
| `business_category`      | `string` | No       | The updated category of the business.           |
| `bp_number`              | `string` | No       | The updated business partner number.            |
| `address_line_1`         | `string` | No       | The updated first line of the home address.     |
| `address_line_2`         | `string` | No       | The updated second line of the home address.    |
| `city`                   | `string` | No       | The updated city of the home address.           |
| `business_address_line_1`| `string` | No       | The updated first line of the business address. |
| `business_address_line_2`| `string` | No       | The updated second line of the business address.|
| `business_city`          | `string` | No       | The updated city of the business address.       |

**Example Result:**

```json
{
    "success": true,
    "message": "Business updated successfully.",
    "data": {
        "id": 1,
        "business_name": "Acme Corp.",
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

- `403 Forbidden` - If the authenticated app is not authorized to update the business.
- `500 Internal Server Error` - If there was an issue updating the business or addresses in the database.

**Description:** This endpoint updates the business and associated home and business addresses for a given business ID.