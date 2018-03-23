# EdUp API

The EdUp API is based on a [REST](https://en.wikipedia.org/wiki/Representational_state_transfer) architecture which makes EdUp API predictable and resource oriented. It uses HTTP built-in features, like HTTP authentication, HTTP verbs (GET, POST, PUT, PATCH, DELETE) and HTTP response codes to allow easy access from any programming language via off-the-shelf libraries and tools.

## Endpoints

* [Courses](api/courses.md) - Manage courses that you create
* [Chapters](api/chapters.md) - Manage chapters in the course
* [Sessions](api/sessions.md) - Manage sessions that you create
* [Watch](api/watch.md) - Public URL to watch the courses

## Identify your account id and api key

To use the API you must provide your username and token in each request via Basic Auth.

Your username and token will be provided in the email with the rules of the exercise.

The only exception is the `watch` endpoint which can be accessed by anyone.

## No XML, just JSON

We only support JSON for serialization of data. This means that you have to send `Content-Type: application/json; charset=utf-8` when you're POSTing, or PATCHing data into EdUp.

## Authentication
As stated previously, EdUp API uses [Basic Auth](https://en.wikipedia.org/wiki/Basic_access_authentication) for authentication.

## Making a request

The base url for this API is http://front-end-exercise.herokuapp.com/.

To create objects using the API each request must include the `Content-Type` header with the value `application/json` and the body must contain data in the JSON format.

```shell
curl -u account_id:token \
  -H 'Content-Type: application/json' \
  http://front-end-exercise.herokuapp.com/ping
```

## Pagination

Some collection calls on our API paginate their results. The first request returns up to 25 records. Check the next page for more results by adding `&page=2`, then `&page=3`, and so on until you get an empty response.

Each page returns a maximum of 25 objects you can increase (up to 50 items per page) or decrease (to 1 per item page) this value adding the `&per_page=50`.

If a given resource is paginated the API will emit the following headers:

|  Header Name  |  Description  |
|---------------|---------------|
| X-Total: 42 | Total number of items found
| X-Total-Pages: 5 | Total number of pages
| X-Page: 3 | The current page
| X-Per-Page: 10 | Amount of items displayed per page
| X-Next-Page: 4 | The number of the next page
| X-Prev-Page: 2 | The number of the previews page
| X-Offset: 10 | The offset to start from

### Example

```shell
http://front-end-exercise.herokuapp.com/courses?page=2&per_page=10
```

## Sort

EdUp API supports sorting for some attributes via query string. To sort a collection just add a `sort=field_name` attribute in the query string and a `-` before the `field_name` if you which descending sorting.

Each sortable entity has supported fields in its own section.

### Example

```shell
http://front-end-exercise.herokuapp.com/chapters?sort=-url # Sort courses by url descending

http://front-end-exercise.herokuapp.com/chapters?sort=name # Sort courses by name ascending
```

## Search

EdUp API supports search and filtering for some attributes via query string. To filter a collection just add a `field_name=something`. Free text searching (`q` attribute) is case insensitive.

Each searchable entity has supported fields in its own section.

### Example

```shell
http://front-end-exercise.herokuapp.com/sessions?q=edup # returns all sessions with 'edup' in name
```

## Handling errors

If EdUp is having trouble, you might see a 5xx error. `500` means that the app is entirely down, but you might also see `502 Bad Gateway`, `503 Service Unavailable`, or `504 Gateway Timeout`. It's your responsibility in all of these cases to retry your request later. If you try to access an unexisting URL you will get the `404 Not Found` error.

When you try to create or update an entity and the the parameters are invalid, it will return a HTTP code `422 Unprocessable entity` with the following response:

```json
{
    "errors": {
        "name": [
            "can't be blank"
        ]
    }
}
```
