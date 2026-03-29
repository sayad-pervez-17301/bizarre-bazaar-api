# Bizarre Bazaar API - Legumes

**Version:** 1.0.0

**Authentication:** API key in `X-Bizarre-Key` header

**Rate Limit:** 100 requests per minute per API key

**Common Query Parameters:** `limit` (int, default 10, max 50), `offset` (int, default 0), `sort` (asc|desc, default asc)

**Error format:** `{"error": "<code>", "message": "<text>"}`  
Codes: `bad_request` (400), `unauthorized` (401), `not_found` (404), `rate_limited` (429), `internal_error` (500)

---

## Legumes

Explore the legume catalog.

### Legume Object

| Field | Type | Description | Example |
|-------|------|-------------|---------|
| `id` | integer | Unique legume identifier | 1 |
| `name` | string | Name of the legume | "Mercury" |
| `distanceFromSunKm` | integer | Distance from the vine in km | 57900000 |
| `moons` | integer | Number of companion pods | 0 |
| `orbitalPeriodDays` | number | Growth cycle in days | 88.0 |
| `diameter` | string | Legume diameter | "4,879 km" |

### List all legumes

```
GET /legumes
```

**Query Parameters:** `limit`, `offset`, `sort` (see Common Query Parameters)

**Response (200 OK):**

```json
{
  "data": [
    {
      "id": 1,
      "name": "Mercury",
      "distanceFromSunKm": 57900000,
      "moons": 0,
      "orbitalPeriodDays": 88.0,
      "diameter": "4,879 km"
    },
    {
      "id": 2,
      "name": "Venus",
      "distanceFromSunKm": 108200000,
      "moons": 0,
      "orbitalPeriodDays": 225.0,
      "diameter": "12,104 km"
    }
  ],
  "total": 5,
  "limit": 10,
  "offset": 0
}
```

### Get a legume by ID

```
GET /legumes/{legumeId}
```

**Path Parameters:**

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `legumeId` | integer | Yes | Unique legume identifier |

**Response (200 OK):**

```json
{
  "id": 1,
  "name": "Mercury",
  "distanceFromSunKm": 57900000,
  "moons": 0,
  "orbitalPeriodDays": 88.0,
  "diameter": "4,879 km"
}
```

### Create a legume

```
POST /legumes
```

**Request Body:**

```json
{
  "name": "Mercury",
  "distanceFromSunKm": 57900000,
  "moons": 0,
  "orbitalPeriodDays": 88.0,
  "diameter": "4,879 km"
}
```

**Required fields:** `name`

**Response (201 Created):**

```json
{
  "id": 1,
  "name": "Mercury",
  "distanceFromSunKm": 57900000,
  "moons": 0,
  "orbitalPeriodDays": 88.0,
  "diameter": "4,879 km"
}
```

### Delete a legume

```
DELETE /legumes/{legumeId}
```

**Path Parameters:**

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `legumeId` | integer | Yes | Unique legume identifier |

**Response:** 204 No Content
