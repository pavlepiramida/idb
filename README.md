# PKB - Responsive Flutter Web / Desktop / Android / iOS

"Personal Knowledge Base" app written on Flutter.

# [>> View DEMO Video](https://www.youtube.com/watch?v=mcXBic0Dl3Q)

## About project

This project was originally made on Django many years ago, then ported to React Web PWA and as of September, 2021 ported to Flutter.

App is compiled to Mac desktop app and iOS app.

Also deployed Web PWA to server to use it on any other devices (phones, tablets). Web, Mac and iOS are ready for use, everything else is supported, but not tested.

PKB has simple and comfortable UI that allows to find anything in few seconds.

I use this UI setup for more than 5 years since it was made on React.

Items (notes) on the left side, tags on the right side and content in the middle.

Features.

-   authentication
-   multi-users with admin access to share with your team members when needed
-   tags
-   content items (notes)
-   quick search
-   keyboard shortcuts
-   uploading images and storing

## Json config that hidden in gitignore

assets/json/config.json

```
{
    "apiUrl": "https://<Your REST API Url>",
    "sentryDSN": "<Your sentry DNS to report errors>"
}
```

## Keyboard shortcuts

```
All shorcuts are listed in app_shortcuts.dart and self explanatory.
```

## I can't opensource backend, it is small part of bigger project.

But backend (REST API) is very simple to implement.

Backend models are matched to frontend models: user.dart, tag.dart, item.dart.

User model on backend additionally has `user_id` field (user who created content item).

## Endpoints (see config.dart)

Login endpoint.

```
POST request.
Params: email, password
Response (200): token
```

User profile endpoint.

```
GET request.
Response (200): User model.
```

Users endpoint

```
GET request.
Response (200): List of User model.
```

Tags endpoint

```
GET request
Response (200): List of Tag model.
```

Items endpoint

```
GET request

Filter params:

search: string (search phrase)
user_id: int (filter by user)
tag_ids: string (comma separated tag ids)

Response (200): List of Item model.


POST request (create item)

Input params:

name: string
content: string
tag_ids: list of ints

Response (201): Created Item model.
```

Item detail endpoint

```
GET request
Response: Item model.

PATCH request (update item)

Input params:

content string
tag_ids: string (list of ints)

Response (200): Updated Item model.

DELETE request
Response (204)
```

image_upload (if you need working with images)
The endpoint is used to generate upload links

```
POST request

Input params:

filename: string
content_type: string

Response (200):

signed_url: url that will be used by Flutter ap for uploading image.
upload_to: the path to image.
```

Content items (notes) are stored in database on backend in markdown format. Flutter app shows content as rendered HTML using `flutter_html` package. I do markdown to HTML convertion on backend using `markdown` Python library, but optionally you can do convertion on Flutter using `flutter_markdown` package.
