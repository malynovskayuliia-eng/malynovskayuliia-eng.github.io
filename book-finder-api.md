---
title: Book Finder API documentation
layout: doc
nav_order: 4
---

# Book Finder API 

The Book Finder API provides access to book metadata, including publication details, ratings, and availability information.

The API supports filtering, pagination, and sorting.

**Base URL**

```
https://api.bookfinder.com/v1
```

**Authentication**

All requests require an API key provided in the request header:

```
Authorization: Bearer YOUR_API_KEY
```

---

## Search books

`GET /books`

Returns a paginated list of books.

---

## Query parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `author` | string | no | Author name filter (partial match supported). |
| `title` | string | no | Book title filter (partial match supported). |
| `isbn` | string | no | ISBN-10 or ISBN-13 identifier. |
| `published_after` | integer | no | Earliest publication year included in the results. |
| `published_before` | integer | no | Latest publication year included in the results. |
| `min_rating` | number | no | Minimum average rating (0-5). |
| `genre` | string | no | Book genre. |
| `language` | string | no | ISO 639-1 language code. |
| `page` | integer | no | Page number of the results. Default: 1. Minimum: 1. |
| `limit` | integer | no | Number of results returned per page. Default: 20. Maximum: 100. |
| `sort_by` | string | no | Field that determines result sorting. One of: `title`, `published_year`, `average_rating`. |
| `sort_order` | string | no | Order in which results are sorted. One of: `asc`, `desc`. |

---

## Example request

```bash
curl -X GET "https://api.bookfinder.com/v1/books?author=orwell&min_rating=4.0&limit=10&sort_by=published_year&sort_order=desc" \
  -H "Authorization: Bearer YOUR_API_KEY"
```

---

## Successful response

`200 OK`

```json
{
  "page": 1,
  "limit": 10,
  "total_count": 42,
  "total_pages": 5,
  "books": [
    {
      "id": "9780451524935",
      "title": "1984",
      "subtitle": null,
      "author": {
        "id": "auth_102",
        "name": "George Orwell"
      },
      "published_year": 1949,
      "isbn_13": "9780451524935",
      "genre": ["dystopian", "political fiction"],
      "language": "en",
      "page_count": 328,
      "average_rating": 4.17,
      "ratings_count": 3256781,
      "available_formats": ["hardcover", "paperback", "ebook"],
      "created_at": "2021-05-12T10:15:30Z",
      "updated_at": "2024-01-03T08:42:11Z"
    }
  ]
}
```

---

## Response schema

| Field | Type | Description |
|--------|------|------------|
| `page` | integer | Current page of results. |
| `limit` | integer | Number of results returned per page. |
| `total_count` | integer | Total number of matching records. |
| `total_pages` | integer | Total number of available pages. |
| `books` | array[Book] | List of book objects. |

### Book 

| Field | Type | Description |
|--------|------|------------|
| `id` | string | Unique book identifier. |
| `title` | string | Book title. |
| `subtitle` | string or null | Book subtitle. |
| `author` | object | Author information. |
| `author.id`| string | Unique author identifier. |
| `author.name`| string | Author name. |
| `published_year` | integer | Year of publication. |
| `isbn_13` | string | ISBN-13 identifier. |
| `genre` | array[string] | List of genres. |
| `language` | string | ISO 639-1 language code. |
| `page_count` | integer | Total number of pages. |
| `average_rating` | number | Average user rating (0-5). |
| `ratings_count` | integer | Total number of ratings. |
| `available_formats` | array[string] | Available formats. |
| `created_at` | string (RFC 3339) | Date and time when the record was created. |
| `updated_at` | string (RFC 3339) | Date and time when the record was last updated. |

---

## Error responses

All error responses return the following structure:

```json
{
  "error": "invalid_parameter",
  "message": "The value of 'min_rating' must be between 0 and 5.",
  "status": 400
}
```

### Error fields

| Field | Type | Description |
|--------|------|------------|
| `error` | string | Error type identifier. |
| `message` | string | Human-readable error description. |
| `status` | integer | HTTP status code. |
