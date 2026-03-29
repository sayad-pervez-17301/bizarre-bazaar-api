# Bizarre Bazaar API - Colors

**Version:** 1.0.0

**Authentication:** API key in `X-Bizarre-Key` header

**Rate Limit:** 100 requests per minute per API key

**Common Query Parameters:** `limit` (int, default 10, max 50), `offset` (int, default 0), `sort` (asc|desc, default asc)

**Error format:** `{"error": "<code>", "message": "<text>"}`  
Codes: `bad_request` (400), `unauthorized` (401), `not_found` (404), `rate_limited` (429), `internal_error` (500)

---

## Colors

Discover and manage colors.

### Color Object

| Field | Type | Description | Example |
|-------|------|-------------|---------|
| `id` | integer | Unique color identifier | 1 |
| `name` | string | Name of the color | "Leonhard Euler" |
| `nationality` | string | Color origin country | "Swiss" |
| `birthYear` | integer | Year the color was first observed | 1707 |
| `knownFor` | string | What this color is famous for | "Euler's formula" |
| `field` | string | Color family | "Analysis" |

### List all colors

```
GET /colors
```

**Query Parameters:** `limit`, `offset`, `sort` (see Common Query Parameters)

**Response (200 OK):**

```json
{
  "data": [
    {
      "id": 1,
      "name": "Leonhard Euler",
      "nationality": "Swiss",
      "birthYear": 1707,
      "knownFor": "Euler's formula",
      "field": "Analysis"
    },
    {
      "id": 2,
      "name": "Carl Friedrich Gauss",
      "nationality": "German",
      "birthYear": 1777,
      "knownFor": "Gaussian distribution",
      "field": "Number Theory"
    }
  ],
  "total": 5,
  "limit": 10,
  "offset": 0
}
```

### Get a color by ID

```
GET /colors/{colorId}
```

**Path Parameters:**

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `colorId` | integer | Yes | Unique color identifier |

**Response (200 OK):**

```json
{
  "id": 1,
  "name": "Leonhard Euler",
  "nationality": "Swiss",
  "birthYear": 1707,
  "knownFor": "Euler's formula",
  "field": "Analysis"
}
```

### Create a color

```
POST /colors
```

**Request Body:**

```json
{
  "name": "Leonhard Euler",
  "nationality": "Swiss",
  "birthYear": 1707,
  "knownFor": "Euler's formula",
  "field": "Analysis"
}
```

**Required fields:** `name`

**Response (201 Created):**

```json
{
  "id": 1,
  "name": "Leonhard Euler",
  "nationality": "Swiss",
  "birthYear": 1707,
  "knownFor": "Euler's formula",
  "field": "Analysis"
}
```

### Delete a color

```
DELETE /colors/{colorId}
```

**Path Parameters:**

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `colorId` | integer | Yes | Unique color identifier |

**Response:** 204 No Content
