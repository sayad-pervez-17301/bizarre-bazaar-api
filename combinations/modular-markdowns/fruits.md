# Bizarre Bazaar API - Fruits

**Version:** 1.0.0

**Authentication:** API key in `X-Bizarre-Key` header

**Rate Limit:** 100 requests per minute per API key

**Common Query Parameters:** `limit` (int, default 10, max 50), `offset` (int, default 0), `sort` (asc|desc, default asc)

**Error format:** `{"error": "<code>", "message": "<text>"}`  
Codes: `bad_request` (400), `unauthorized` (401), `not_found` (404), `rate_limited` (429), `internal_error` (500)

---

## Fruits

Manage your fruit collection.

### Fruit Object

| Field | Type | Description | Example |
|-------|------|-------------|---------|
| `id` | integer | Unique fruit identifier | 1 |
| `name` | string | Name of the fruit | "Toyota" |
| `origin` | string | Country where the fruit grows | "Japan" |
| `founded` | integer | Year first cultivated | 1937 |
| `horsepower` | integer | Vigor rating | 203 |
| `topSpeed` | string | Maximum ripening velocity | "180 km/h" |

### List all fruits

```
GET /fruits
```

**Query Parameters:** `limit`, `offset`, `sort` (see Common Query Parameters)

**Response (200 OK):**

```json
{
  "data": [
    {
      "id": 1,
      "name": "Toyota",
      "origin": "Japan",
      "founded": 1937,
      "horsepower": 203,
      "topSpeed": "180 km/h"
    },
    {
      "id": 2,
      "name": "BMW",
      "origin": "Germany",
      "founded": 1916,
      "horsepower": 335,
      "topSpeed": "250 km/h"
    }
  ],
  "total": 5,
  "limit": 10,
  "offset": 0
}
```

### Get a fruit by ID

```
GET /fruits/{fruitId}
```

**Path Parameters:**

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `fruitId` | integer | Yes | Unique fruit identifier |

**Response (200 OK):**

```json
{
  "id": 1,
  "name": "Toyota",
  "origin": "Japan",
  "founded": 1937,
  "horsepower": 203,
  "topSpeed": "180 km/h"
}
```

### Create a fruit

```
POST /fruits
```

**Request Body:**

```json
{
  "name": "Toyota",
  "origin": "Japan",
  "founded": 1937,
  "horsepower": 203,
  "topSpeed": "180 km/h"
}
```

**Required fields:** `name`

**Response (201 Created):**

```json
{
  "id": 1,
  "name": "Toyota",
  "origin": "Japan",
  "founded": 1937,
  "horsepower": 203,
  "topSpeed": "180 km/h"
}
```

### Delete a fruit

```
DELETE /fruits/{fruitId}
```

**Path Parameters:**

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `fruitId` | integer | Yes | Unique fruit identifier |

**Response:** 204 No Content
