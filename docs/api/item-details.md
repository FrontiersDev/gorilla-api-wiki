# Item Details & Downloads

This section covers how to retrieve metadata for specific items and how to download their associated assets (3D models, icons, and bundles).

---

## 1. Get Item Details

Retrieves the full metadata for a specific cosmetic item by its unique ID.

**Endpoint:** `GET /api/cosmetics/:id`

### Parameters

| Parameter | Type | In | Description |
| :--- | :--- | :--- | :--- |
| `id` | `string` | URL Path | **Required.** The unique ID of the item (e.g., `party-hat`, `admin-badge`). |

### Example Request

```http
GET http://localhost:3000/api/cosmetics/party-hat
```

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

## 2. Download Assets

Once you have the item's ID or filename, you can use these endpoints to download the actual files.

A. Download 3D Model
Directly downloads the .fbx model file for an item.

Endpoint: ```GET /api/cosmetics/:id/download```

Success: Triggers a file download (e.g., party-hat.fbx).

Error: Returns 404 if the item exists but has no model file attached.

B. Download Icon
To get the icon, you simply access the static asset path using the filename found in the JSON response.

Endpoint: ```GET /assets/icons/:filename```

Example:

HTTP

```http://localhost:3000/assets/icons/party-hat.png```

C. Download ZIP Bundle
Creates a compressed .zip file containing the item's JSON Data, Icon, and 3D Model (if available). This is extremely useful for "Download All" buttons or archiving assets.

Endpoint: ```GET /api/cosmetics/:id/zip```

Example Request:

HTTP

```GET http://localhost:3000/api/cosmetics/party-hat/zip```

### Content of party-hat.zip:

- party-hat.json (Metadata)

- party-hat.png (Icon)

- party-hat.fbx (3D Model)