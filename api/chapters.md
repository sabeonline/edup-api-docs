# Chapters

Chapter CRUD endpoints. All chapter activities are scoped to a chapter. It means you cannot list all existing chapters you created but only the chapters in a particular chapter.

## Listing all chapters

```shell
GET /courses/:course_id/chapters/
```

### Response

```json
[
  {
    "id": 1,
    "name": "How EdUp Works",
    "url": "https://youtu.be/1RiythWDSUQ",
    "course_id": 1,
    "created_at": "2018-03-22T10:00:39.026Z"
  },
  {
    "id": 2,
    "name": "Our courses",
    "url": "https://youtu.be/nWoiAnHd1ic",
    "course_id": 1,
    "created_at": "2018-03-22T10:00:39.032Z"
  }
]
```

### Chapter fields description

|  Name  |  Type  |  Description  |
|--------|--------|---------------|
| id | id | ID of the chapter
| name | string | Name of the chapter
| url | string | URL of the video
| course_id | id | ID of the course which the chapter belongs
| created_at | timestamp | Date of creation of the chapter

Chapters are [searchable](/README.md#search) and [sortable](/README.md#sort) as described in main page.

* **Searchable fields**

|  field  |  type  |  description  |
|---------|--------|---------------|
| q | string | Free text. Searches in chapter name, id and url |

* **Sortable fields**
  * name (default)
  * id
  * url
  * created_at

## Showing one chapter

```shell
GET /courses/:course_id/chapters/:chapter_id
```

### Response

```json
{
  "id": 1,
  "name": "How EdUp Works",
  "url": "https://youtu.be/1RiythWDSUQ",
  "course_id": 1,
  "created_at": "2018-03-22T10:00:39.026Z"
}
```

## Creating a chapter

```shell
POST /courses/:course_id/chapters/
```

### Payload

```json
{
  "name": "My awesome new chapter",
  "url": "https://youtu.be/RZQMkP80Qlw",
}
```

### Response

HTTP code: `201`

```json
{
  "id": 3,
  "name": "My awesome new chapter",
  "url": "https://youtu.be/RZQMkP80Qlw",
  "course_id": 1,
  "created_at": "2018-03-22T10:00:39.026Z"
}
```

## Updating a chapter

```shell
PATCH /courses/:course_id/chapters/:chapter_id
```

### Payload

```json
{
  "name": "My awesome new chapter updated",
  "url": "https://youtu.be/RZQMkP80Qlw"
}
```

### Response

HTTP code: `204 no content`

## Deleting a chapter

```shell
DELETE /courses/:course_id/chapters/:chapter_id
```

### Response

HTTP code: `204 no content`

## Moving chapters

All chapters are ordered and when creating a new chapter it will always be inserted at the last position. To allow the need of inserting a new chapter in the middle of the course structure, there are two endpoints to do the job:

```shell
PUT /courses/:course_id/chapters/:chapter_id/move_up
PUT /courses/:course_id/chapters/:chapter_id/move_down
```

### Response

HTTP code: `204 no content`
