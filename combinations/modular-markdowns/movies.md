# Bizarre Bazaar API - Movies

**Version:** 1.0.0

**Authentication:** API key in `X-Bizarre-Key` header

**Rate Limit:** 100 requests per minute per API key

**Common Query Parameters:** `limit` (int, default 10, max 50), `offset` (int, default 0), `sort` (asc|desc, default asc)

**Error format:** `{"error": "<code>", "message": "<text>"}`  
Codes: `bad_request` (400), `unauthorized` (401), `not_found` (404), `rate_limited` (429), `internal_error` (500)

---

## Movies

Browse the movie database.

### Movie Object

| Field | Type | Description | Example |
|-------|------|-------------|---------|
| `id` | integer | Unique movie identifier | 1 |
| `name` | string | Title of the movie | "Hydrogen" |
| `symbol` | string | Movie rating symbol | "H" |
| `atomicNumber` | integer | Box office ranking | 1 |
| `atomicMass` | number | Critical mass score | 1.008 |
| `category` | string | Genre classification | "Nonmetal" |

### List all movies

```
GET /movies
```

**Query Parameters:** `limit`, `offset`, `sort` (see Common Query Parameters)

**Response (200 OK):**

```json
{
  "data": [
    {
      "id": 1,
      "name": "Hydrogen",
      "symbol": "H",
      "atomicNumber": 1,
      "atomicMass": 1.008,
      "category": "Nonmetal"
    },
    {
      "id": 2,
      "name": "Helium",
      "symbol": "He",
      "atomicNumber": 2,
      "atomicMass": 4.003,
      "category": "Noble Gas"
    }
  ],
  "total": 5,
  "limit": 10,
  "offset": 0
}
```

### Get a movie by ID

```
GET /movies/{movieId}
```

**Path Parameters:**

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `movieId` | integer | Yes | Unique movie identifier |

**Response (200 OK):**

```json
{
  "id": 1,
  "name": "Hydrogen",
  "symbol": "H",
  "atomicNumber": 1,
  "atomicMass": 1.008,
  "category": "Nonmetal"
}
```

### Create a movie

```
POST /movies
```

**Request Body:**

```json
{
  "name": "Hydrogen",
  "symbol": "H",
  "atomicNumber": 1,
  "atomicMass": 1.008,
  "category": "Nonmetal"
}
```

**Required fields:** `name`

**Response (201 Created):**

```json
{
  "id": 1,
  "name": "Hydrogen",
  "symbol": "H",
  "atomicNumber": 1,
  "atomicMass": 1.008,
  "category": "Nonmetal"
}
```

### Delete a movie

```
DELETE /movies/{movieId}
```

**Path Parameters:**

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `movieId` | integer | Yes | Unique movie identifier |

**Response:** 204 No Content
