## Store a New Profile

### Request

**Method:** `POST`

**Path:** `/api/v1/app/profiles`

**Authorization:**

Bearer token required.

**Parameters:**

| Name        | Type     | Required | Description                                                |
|-------------|----------|----------|--------------------------------------------------------------|
| `phone`     | `string` | Yes      | The user's phone number, must be a valid Zimbabwean phone number and unique in the system. |
| `first_name`| `string` | Yes      | The user's first name, maximum length of 255 characters.   |
| `last_name` | `string` | Yes      | The user's last name, maximum length of 255 characters.    |
| `id_number` | `string` | Yes      | The user's national ID number, must be unique in the system. |
| `dob`       | `string` | Yes      | The user's date of birth in the format `d/m/Y`. The user must be at least 11 years old. |
| `email`     | `string` | No       | The user's email address, must be a valid email and unique in the system. |

**Example Result:**

```json
{
    "success": true,
    "message": "Profile was created successfully. User number sent on WhatsApp",
    "data": {
        "phone": "26377123456",
        "first_name": "John",
        "last_name": "Doe",
        "dob": "27/12/1990",
        "id_number": "12-1885994X55",
        "email": "john@example.com",
        "created_at": "2023-04-01T10:15:30.000000Z",
        "updated_at": "2023-04-01T10:15:30.000000Z"
    }
}
```

**Status Code:** `201 Created`

**Errors:**

- `422 Unprocessable Entity` - If any of the required fields are missing or invalid.
- `500 Internal Server Error` - If there was an issue sending the user's number via SMS/WhatsApp.

**Notes:**

- The user's phone number is sent to them via WhatsApp after the profile is created successfully.
- The `validate_phone` and `zw_unique_profiles` validation rules are custom rules specific to this application.

