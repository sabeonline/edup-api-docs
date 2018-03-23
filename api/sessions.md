# Sessions

Session CRUD endpoints. In a session you can add and remove courses. Each session is shared to users through a public URL. All the existing courses in the session will be available for the users who access the link.

## Listing all sessions

```shell
GET /sessions/
```

### Response

```json
[
  {
    "id": 1,
    "name": "Self-learning courses",
    "status": "published",
    "public_url": "http://front-end-exercise.herokuapp.com/watch/0_N8y-iF",
    "created_at": "2018-03-22T10:00:39.093Z"
  },
  {
    "id": 2,
    "name": "Technology",
    "status": "draft",
    "public_url": "http://front-end-exercise.herokuapp.com/watch/qieL1a27",
    "created_at": "2018-03-22T10:01:27.601Z"
  }
]
```

### Session fields description

|  Name  |  Type  |  Description  |
|--------|--------|---------------|
| id | id | ID of the session
| name | string | Name of the session
| public_url | string | The URL that will be shared to the courses students
| created_at | timestamp | Date of creation of the session

Sessions are [searchable](/README.md#search) and [sortable](/README.md#sort) as described in main page.

* **Searchable fields**

|  field  |  type  |  description  |
|---------|--------|---------------|
| q | string | Free text. Searches in session name and id and token |
| status | string | One of the 3 values: `draft`, `published` or `archived` |

* **Sortable fields**
  * name (default)
  * id
  * status
  * created_at

## Showing one session

```shell
GET /sessions/:session_id
```

### Response

```json
{
  "id": 1,
  "name": "Self-learning courses",
  "status": "published",
  "public_url": "http://front-end-exercise.herokuapp.com/watch/0_N8y-iF",
  "created_at": "2018-03-22T10:00:39.093Z",
  "courses": [
    {
      "id": 1,
      "name": "Welcome to EdUp",
      "created_at": "2018-03-22T10:00:39.011Z"
    }
  ]
}
```

## Creating a session

```shell
POST /sessions/
```

### Payload

```json
{
  "name": "My awesome new session"
}
```

### Response

HTTP code: `201`

```json
{
  "id": 3,
  "name": "My awesome new session",
  "created_at": "2018-03-22T10:00:39.011Z"
}
```

## Updating a session

```shell
PATCH /sessions/:session_id
```

### Payload

```json
{
  "name": "My awesome new session updated"
}
```

### Response

HTTP code: `204 no content`

## Deleting a session

```shell
DELETE /sessions/:session_id
```

### Response

HTTP code: `204 no content`

## Changing the status of a session

Sessions have statuses. Only published sessions can be viewed by the users. To change to the existing statuses you have three corresponding endpoints.

```shell
PUT /sessions/:session_id/publish # sets the status to pubished
PUT /sessions/:session_id/draft # sets the status to draft
PUT /sessions/:session_id/archive # sets the status to archived
```

### Response

HTTP code: `204 no content`

## Adding a course to a session

```shell
POST /sessions/:session_id/courses/:course_id
```

### Response

HTTP code: `204 no content`

## Removing a course from a session

```shell
DELETE /sessions/:session_id/courses/:course_id
```

### Response

HTTP code: `204 no content`
