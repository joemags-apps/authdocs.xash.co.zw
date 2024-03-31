# Profile Registration

The Profile Registration process allows users to create a new profile in the system. It involves two main steps: submitting the user's personal details and setting a password for the account.

### NOTE
- The `phone` parameter should be in E.164 format (e.g., '263771234567') without the leading '+' or '00'.

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


## Resend User Number

This endpoint allows an authenticated app to resend the user's number to them via WhatsApp in case the initial attempt failed or if the user didn't receive it.

### Request

**Method:** `POST`

**Path:** `/api/v1/app/profiles/resend/{phone}`

**Authorization:**

Bearer token required.

**Parameters:**

| Name    | Type     | Required | Description                                      |
|---------|----------|----------|--------------------------------------------------|
| `phone` | `string` | Yes      | The user's phone number to resend the user number to. |

**Example Result:**

```json
{
    "success": true,
    "message": "User number was sent successfully. User number sent on WhatsApp"
}
```

**Status Code:** `200 OK`

**Errors:**

- `403 Forbidden` - If the user's profile does not belong to the authenticated app.
- `419 Too Many Attempts` - If the user's password has already been set. They should use the login page instead.
- `500 Internal Server Error` - If there was an issue sending the user's number via SMS/WhatsApp.

**Notes:**

- This endpoint can only be used for profiles that have not yet set a password.
- If the user's number is resent successfully, a log entry is created with the user's details and a flag indicating if the SMS was sent or not.

## Set Password

### Request

**Method:** `POST`

**Path:** `/api/v1/app/profiles/set-password`

**Authorization:**

Bearer token required.

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

## Update Profile

This endpoint allows an authenticated app to update a user profile that belongs to the app.

### Request

**Method:** `PUT`

**Path:** `/api/v1/app/profiles/{phone}`

**Authorization:**

Bearer token required.

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

# Delete Profile

This endpoint allows an authenticated app to delete a user profile that belongs to the app.

### Request

**Method:** `DELETE`

**Path:** `/api/v1/app/profiles/{phone}`

**Authorization:**

Bearer token required.

**Parameters:**

| Name    | Type     | Required | Description                 |
|---------|----------|----------|-----------------------------|
| `phone` | `string` | Yes      | The user's phone number in E.164 format without the leading '+' or '00'.    |

**Example Result:**

```json
{
    "success": true,
    "message": "Profile was deleted successfully."
}
```

**Status Code:** `200 OK`

**Errors:**

- `403 Forbidden` - If the user's profile does not belong to the authenticated app.

**Notes:**

- This endpoint only allows deleting profiles that belong to the authenticated app.
- Once a profile is deleted, all associated data (such as business information) will also be removed from the system.
- The `phone` parameter should be in E.164 format (e.g., '263771234567') without the leading '+' or '00'.