## Set Password

### Request

**Method:** `POST`

**Path:** `/api/v1/app/profiles/set-password`

**Parameters:**

| Name         | Type     | Required | Description                                                |
|--------------|----------|----------|--------------------------------------------------------------|
| `user_number`| `integer`| Yes      | The user's number that was sent to them previously.       |
| `password`   | `string` | Yes      | The new password to set for the user's account.           |
| `password_confirmation` | `string` | Yes | The confirmation of the new password, must match `password`. |

**Example Result:**

```json
{
    "success": true,
    "message": "Password was set successfully.",
    "data": {
        "phone": "26377123456",
        "first_name": "John",
        "last_name": "Doe",
        "dob": "27/12/1990",
        "id_number": "12-1885994X55",
        "email": "john@example.com",
        "created_at": "2023-04-01T10:15:30.000000Z",
        "updated_at": "2023-04-01T10:20:45.000000Z"
    }
}
```

**Status Code:** `200 OK`

**Errors:**

- `404 Not Found` - If the `user_number` is not found in the system.
- `403 Forbidden` - If the user's profile does not belong to the authenticated app.
- `419 Too Many Attempts` - If the user's password has already been set.
- `422 Unprocessable Entity` - If any of the required fields are missing or invalid, or if the `password` and `password_confirmation` do not match.

**Notes:**

- The `user_number` must be a valid number that was sent to the user previously when their profile was created.
- The `Password` validation rules ensure that the password meets the required complexity.

Sure, I've updated the notes section with the information about the phone number format.
