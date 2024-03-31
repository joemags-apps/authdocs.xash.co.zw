# Business Management

The Business Management functionality allows authenticated apps to manage businesses and their associated addresses for user profiles.

### NOTE
- The `phone` parameter should be in E.164 format (e.g., '263771234567') without the leading '+' or '00'.

## Get Business Categories

### Request

**Method:** `GET`

**Path:** `/api/v1/app/business/categories`

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

## Get Profile's Business

### Request

**Method:** `GET`

**Path:** `/api/v1/app/business/{profile}`

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