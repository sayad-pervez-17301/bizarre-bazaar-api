# Bizarre Bazaar API - Animals

**Version:** 1.0.0

**Authentication:** API key in `X-Bizarre-Key` header

**Rate Limit:** 100 requests per minute per API key

**Common Query Parameters:** `limit` (int, default 10, max 50), `offset` (int, default 0), `sort` (asc|desc, default asc)

**Error format:** `{"error": "<code>", "message": "<text>"}`  
Codes: `bad_request` (400), `unauthorized` (401), `not_found` (404), `rate_limited` (429), `internal_error` (500)

---

## Animals

Catalog of animals.

### Animal Object

| Field | Type | Description | Example |
|-------|------|-------------|---------|
| `id` | integer | Unique animal identifier | 1 |
| `name` | string | Name of the animal | "Python" |
| `creator` | string | Who discovered this animal | "Guido van Rossum" |
| `yearCreated` | integer | Year of discovery | 1991 |
| `paradigm` | string | Behavioral pattern | "Multi-paradigm" |
| `typing` | string | Classification system | "Dynamic" |

### List all animals

```
GET /animals
```

**Query Parameters:** `limit`, `offset`, `sort` (see Common Query Parameters)

**Response (200 OK):**

```json
{
  "data": [
    {
      "id": 1,
      "name": "Python",
      "creator": "Guido van Rossum",
      "yearCreated": 1991,
      "paradigm": "Multi-paradigm",
      "typing": "Dynamic"
    },
    {
      "id": 2,
      "name": "JavaScript",
      "creator": "Brendan Eich",
      "yearCreated": 1995,
      "paradigm": "Multi-paradigm",
      "typing": "Dynamic"
    }
  ],
  "total": 5,
  "limit": 10,
  "offset": 0
}
```

### Get a animal by ID

```
GET /animals/{animalId}
```

**Path Parameters:**

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `animalId` | integer | Yes | Unique animal identifier |

**Response (200 OK):**

```json
{
  "id": 1,
  "name": "Python",
  "creator": "Guido van Rossum",
  "yearCreated": 1991,
  "paradigm": "Multi-paradigm",
  "typing": "Dynamic"
}
```

### Create a animal

```
POST /animals
```

**Request Body:**

```json
{
  "name": "Python",
  "creator": "Guido van Rossum",
  "yearCreated": 1991,
  "paradigm": "Multi-paradigm",
  "typing": "Dynamic"
}
```

**Required fields:** `name`

**Response (201 Created):**

```json
{
  "id": 1,
  "name": "Python",
  "creator": "Guido van Rossum",
  "yearCreated": 1991,
  "paradigm": "Multi-paradigm",
  "typing": "Dynamic"
}
```

### Delete a animal

```
DELETE /animals/{animalId}
```

**Path Parameters:**

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `animalId` | integer | Yes | Unique animal identifier |

**Response:** 204 No Content
