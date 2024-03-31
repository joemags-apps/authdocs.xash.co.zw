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
