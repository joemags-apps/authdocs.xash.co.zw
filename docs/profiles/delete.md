
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