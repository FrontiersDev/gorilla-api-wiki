# Get Single Item

Retrieves details for a specific cosmetic item by its unique ID.

**Endpoint:** `GET /api/cosmetics/:id`

## Parameters

| Parameter | Type | In | Description |
| :--- | :--- | :--- | :--- |
| `id` | `string` | URL Path | **Required.** The unique ID of the item (e.g., `party-hat`, `admin-badge`). |

## Example Request

```http
GET http://localhost:3000/api/cosmetics/party-hat
```

## Example Response (JSON)

```json
{
  "id": "party-hat",
  "name": "Party Hat",
  "slot": "Hat",
  "price": 500,
  "currency": "Shiny Rocks",
  "files": {
    "icon": "party-hat.png",
    "model": "party-hat.fbx"
  }
}
```

## Errors
404 Not Found: If the ID does not exist in the database.