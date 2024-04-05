# Authenticate Profile

This endpoint allows authenticating a user profile using their user number and password.

### Request

**Method:** `POST`

**Path:** `/api/v1/app/profiles/authenticate`

**Authorization:**

Bearer token required.

**Parameters:**

| Name         | Type     | Required | Description                                |
|--------------|----------|----------|--------------------------------------------|
| `user_number`| `integer`| Yes      | The user's number that was sent to them previously. |
| `password`   | `string` | Yes      | The user's password.                      |

**Example Result:**

```json
{
    "success": true,
    "message": "User was authenticated successfully",
    "data": {
        "phone": "26377123456",
        "first_name": "John",
        "last_name": "Doe",
        "id_number": "12-1885994X55",
        "dob": "27/12/1990"
    }
}
```

**Status Code:** `200 OK`

**Errors:**

- `404 Not Found` - If the provided user number is not found in the system.

**Notes:**

- This endpoint authenticates the user using the provided user number and password.
- Upon successful authentication, success message is returned.
- The response includes the authenticated user's profile data, such as phone number, name, ID number, and date of birth.