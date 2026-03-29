# Bizarre Bazaar API

**Version:** 1.0.0

The Bizarre Bazaar API is a RESTful service for managing six unique collections: Fruits, Vegetables, Legumes, Colors, Animals, and Movies. Each collection supports full CRUD operations with pagination and sorting.

## Authentication

All requests must include an API key in the `X-Bizarre-Key` header.

```http
GET /fruits HTTP/1.1
Host: api.example.com
X-Bizarre-Key: your-api-key-here
```

## Base URL

```
https://{host}/
```

## Rate Limiting

- 100 requests per minute per API key
- Rate-limit headers in every response:
  - `X-RateLimit-Limit` - Maximum requests per window
  - `X-RateLimit-Remaining` - Remaining requests in current window
  - `X-RateLimit-Reset` - Unix timestamp when the window resets

## Common Query Parameters

All list endpoints accept these query parameters:

| Parameter | Type    | Default | Description                |
|-----------|---------|---------|----------------------------|
| `limit`   | integer | 10      | Max items to return (1-50) |
| `offset`  | integer | 0       | Number of items to skip    |
| `sort`    | string  | asc     | Sort order: `asc` or `desc`|

## Error Responses

All errors follow a consistent JSON structure:

```json
{
  "error": "error_code",
  "message": "Human-readable description"
}
```

| Status | Code             | Description                       |
|--------|------------------|-----------------------------------|
| 400    | `bad_request`    | Invalid request parameters        |
| 401    | `unauthorized`   | Missing or invalid API key        |
| 404    | `not_found`      | Requested resource does not exist |
| 429    | `rate_limited`   | Too many requests                 |
| 500    | `internal_error` | Unexpected server error           |

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
