# Downloads & ZIPs

The API provides direct access to asset files and can dynamically bundle them into ZIP archives for easy downloading.

## 1. Download 3D Model

Directly downloads the `.fbx` model file for an item.

**Endpoint:** `GET /api/cosmetics/:id/download`

- **Success:** Triggers a file download (e.g., `party-hat.fbx`).
- **Error:** Returns `404` if the item exists but has no model file attached.

## 2. Download Icon

To get the icon, you simply access the static asset path.

**Endpoint:** `GET /assets/icons/:filename`

**Example:**
```http
http://localhost:3000/assets/icons/party-hat.png
```


## 3. Download ZIP Bundle

Creates a compressed .zip file containing the item's JSON Data, Icon, and 3D Model (if available). This is useful for "Download All" buttons.

Endpoint: GET /api/cosmetics/:id/zip

Example Request:

HTTP

```
GET http://localhost:3000/api/cosmetics/party-hat/zip```

### Content of party-hat.zip:

- party-hat.json (Metadata)

- party-hat.png (Icon)

- party-hat.fbx (3D Model)