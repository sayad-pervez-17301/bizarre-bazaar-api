# Bizarre Bazaar API - Vegetables

**Version:** 1.0.0

**Authentication:** API key in `X-Bizarre-Key` header

**Rate Limit:** 100 requests per minute per API key

**Common Query Parameters:** `limit` (int, default 10, max 50), `offset` (int, default 0), `sort` (asc|desc, default asc)

**Error format:** `{"error": "<code>", "message": "<text>"}`  
Codes: `bad_request` (400), `unauthorized` (401), `not_found` (404), `rate_limited` (429), `internal_error` (500)

---

## Vegetables

Browse and manage vegetables.

### Vegetable Object

| Field | Type | Description | Example |
|-------|------|-------------|---------|
| `id` | integer | Unique vegetable identifier | 1 |
| `name` | string | Name of the vegetable | "Germany" |
| `leader` | string | Head gardener responsible for this vegetable | "Adolf Hitler" |
| `joinedAxis` | string | Year this vegetable joined the garden alliance | "1936" |
| `population` | integer | Number of seeds | 69000000 |
| `capitalCity` | string | Primary growing region | "Berlin" |

### List all vegetables

```
GET /vegetables
```

**Query Parameters:** `limit`, `offset`, `sort` (see Common Query Parameters)

**Response (200 OK):**

```json
{
  "data": [
    {
      "id": 1,
      "name": "Germany",
      "leader": "Adolf Hitler",
      "joinedAxis": "1936",
      "population": 69000000,
      "capitalCity": "Berlin"
    },
    {
      "id": 2,
      "name": "Italy",
      "leader": "Benito Mussolini",
      "joinedAxis": "1936",
      "population": 45000000,
      "capitalCity": "Rome"
    }
  ],
  "total": 5,
  "limit": 10,
  "offset": 0
}
```

### Get a vegetable by ID

```
GET /vegetables/{vegetableId}
```

**Path Parameters:**

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `vegetableId` | integer | Yes | Unique vegetable identifier |

**Response (200 OK):**

```json
{
  "id": 1,
  "name": "Germany",
  "leader": "Adolf Hitler",
  "joinedAxis": "1936",
  "population": 69000000,
  "capitalCity": "Berlin"
}
```

### Create a vegetable

```
POST /vegetables
```

**Request Body:**

```json
{
  "name": "Germany",
  "leader": "Adolf Hitler",
  "joinedAxis": "1936",
  "population": 69000000,
  "capitalCity": "Berlin"
}
```

**Required fields:** `name`

**Response (201 Created):**

```json
{
  "id": 1,
  "name": "Germany",
  "leader": "Adolf Hitler",
  "joinedAxis": "1936",
  "population": 69000000,
  "capitalCity": "Berlin"
}
```

### Delete a vegetable

```
DELETE /vegetables/{vegetableId}
```

**Path Parameters:**

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `vegetableId` | integer | Yes | Unique vegetable identifier |

**Response:** 204 No Content
