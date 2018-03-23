# Courses

Course CRUD endpoints.

## Listing all courses

```shell
GET /courses/
```

### Response

```json
[
  {
    "id": 1,
    "name": "Welcome to EdUp",
    "created_at": "2018-03-22T10:00:39.011Z"
  },
  {
    "id": 2,
    "name": "How to build an API",
    "created_at": "2018-03-22T10:00:39.043Z"
  }
]
```

### Course fields description

|  Name  |  Type  |  Description  |
|--------|--------|---------------|
| id | id | ID of the course
| name | string | Name of the course
| created_at | timestamp | Date of creation of the course

Courses are [searchable](/README.md#search) and [sortable](/README.md#sort) as described in main page.

* **Searchable fields**

|  field  |  type  |  description  |
|---------|--------|---------------|
| q | string | Free text. Searches in course name and id |

* **Sortable fields**
  * name (default)
  * id
  * created_at

## Showing one course

```shell
GET /courses/:course_id
```

### Response

```json
{
  "id": 1,
  "name": "Welcome to EdUp",
  "created_at": "2018-03-22T10:00:39.011Z"
}
```

## Creating a course

```shell
POST /courses/
```

### Payload

```json
{
  "name": "My awesome new course"
}
```

### Response

HTTP code: `201`

```json
{
  "id": 3,
  "name": "My awesome new course",
  "created_at": "2018-03-22T10:00:39.011Z"
}
```

## Updating a course

```shell
PATCH /courses/:course_id
```

### Payload

```json
{
  "name": "My awesome new course updated"
}
```

### Response

HTTP code: `204 no content`

## Deleting a course

```shell
DELETE /courses/:course_id
```

### Response

HTTP code: `204 no content`
