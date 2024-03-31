# List App's Profiles

## Request

**Method:** `GET`

**Path:** `/api/v1/app/profiles`

**Authorization:**

Bearer token required.

**Parameters:** None

**Example Result:**

```json
{
    "data": [
        {
            "phone": "263775123456",
            "first_name": "John",
            "last_name": "Doe",
            "dob": "27/12/1990",
            "id_number": "12-1885994X55",
            "email": null,
            "user_number": 12345
        },
        {
            "phone": "263772123456",
            "first_name": "Jane",
            "last_name": "Doe",
            "dob": "15/04/1985",
            "id_number": "63-123456X78",
            "email": "jane@example.com",
            "user_number": 67890
        }
    ]
}
```

**Status Code:** `200 OK`

**Description:** This endpoint retrieves a list of user profiles associated with the authenticated app.

**Notes:**

- Only profiles belonging to the authenticated app are returned.
- The response includes the user's phone number, name, date of birth, ID number, email, and user number.