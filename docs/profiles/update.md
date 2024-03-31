## Update Profile

This endpoint allows an authenticated app to update a user profile that belongs to the app.

### Request

**Method:** `PUT`

**Path:** `/api/v1/app/profiles/{phone}`

**Parameters:**

| Name        | Type     | Required | Description                                                |
|-------------|----------|----------|--------------------------------------------------------------|
| `phone`     | `string` | Yes      | The user's phone number in E.164 format without the leading '+' or '00'. |
| `first_name`| `string` | No       | The updated first name of the user.                       |
| `last_name` | `string` | No       | The updated last name of the user.                        |
| `id_number` | `string` | No       | The updated national ID number of the user.              |
| `dob`       | `string` | No       | The updated date of birth of the user in the format `d/m/Y`. |
| `email`     | `string` | No       | The updated email address of the user.                    |

**Example Result:**

```json
{
    "success": true,
    "message": "Profile was updated successfully.",
    "data": {
        "phone": "26377123456",
        "first_name": "John",
        "last_name": "Updated Last Name",
        "dob": "27/12/1990",
        "id_number": "12-1885994X55",
        "email": "john@example.com",
        "created_at": "2023-04-01T10:15:30.000000Z",
        "updated_at": "2023-04-01T11:20:45.000000Z"
    }
}
```

**Status Code:** `200 OK`

**Errors:**

- `403 Forbidden` - If the user's profile does not belong to the authenticated app.
- `422 Unprocessable Entity` - If any of the provided fields are invalid (e.g., invalid date format, email format, etc.).

**Notes:**

- This endpoint only allows updating profiles that belong to the authenticated app.
- Only the fields provided in the request will be updated; any fields not included will remain unchanged.
- The `phone` parameter should be in E.164 format (e.g., '263771234567') without the leading '+' or '00'.
