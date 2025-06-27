# API Endpoints

## Table of Contents
- [Job Entries](#job-entries)
- [Individual Job Entry](#get-job-entry-by-key)
- [Categories](#categories)

---
This is here to document all the API endpoints used in this project

## Job Entries

**Endpoint:** `GET /api/job-entries`

### Response Example

```json
[
  {
    "id": number,
    "title": "string",
    "description": "string",
    "expiration": "string",
    "category": "string",
    "created_at": "string",
    "job_posting_key": "string"
  }
]


```

### Query Parameters

| Parameter        | Type    | Required | Description                                                                 |
|------------------|---------|----------|-----------------------------------------------------------------------------|
| `includeExpired` | boolean | No       | If `true`, returns expired job entries as well. Defaults to `false`.        |

---

## Get Job Entry by Key

**Endpoint:** `GET /api/job-entries/?key=[key]`

**Example:** `KEY=devops-engineer-7`
### Description

Fetch a single job entry from the `job_entries` table using the unique `job_posting_key`.  

### Query Parameters

| Parameter        | Type    | Required | Description                                                                 |
|------------------|---------|----------|-----------------------------------------------------------------------------|
| `key`            | string  | Yes      | Unique job posting key used to identify the job entry.                      |


### Behavior

- Returns the job entry matching the specified `key`.
- By default (`includeExpired` not set or `false`), returns only non-expired jobs (expiration date in the future or null).
- Returns HTTP 400 if `key` is missing.
- Returns HTTP 500 if a database error occurs.


### Response

- **200 OK**: JSON object with job entry details:

  ```json
  {
    "id": number,
    "title": string,
    "description": string,
    "expiration": string | null,
    "category": string,
    "created_at": string,
    "job_posting_key": string
  }


---
## Categories

**EndPoint:** `GET /api/categories`

### Description

Retrieve a list of all categories from the `categories` table, ordered by category name in descending order.

### Behavior

- Fetches `category_name` from the `categories` table.
- Orders results by `category_name` descending.
- Returns HTTP 500 with an error message if the database query fails.

### Response

- **200 OK**: JSON array of category objects:

  ```json
  [
    { "category_name": "Marketing" },
    { "category_name": "Engineering" },
    { "category_name": "Design" }
  ]
