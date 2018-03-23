# Watch

This is the public endpoint to show your courses to the students.

## Showing one session

```shell
GET /watch/:session_token
```

### Response

```json
{
  "name": "Self-learning courses",
  "courses": [
    {
      "name": "Welcome to EdUp",
      "chapters": [
        {
          "name": "How EdUp Works",
          "url": "https://youtu.be/1RiythWDSUQ",
        },
        {
          "name": "Our courses",
          "url": "https://youtu.be/nWoiAnHd1ic",
        }
      ]
    }
  ]
}
```

### Session fields description

Courses listed in this session are [searchable](/README.md#search) and [sortable](/README.md#sort) as described in main page.

* **Searchable fields**

|  field  |  type  |  description  |
|---------|--------|---------------|
| q | string | Free text. Searches in courses name and chapters name |

* **Sortable fields**
  * name (default)
