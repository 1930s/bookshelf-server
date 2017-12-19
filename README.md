[![codebeat badge](https://codebeat.co/badges/29a7843e-3710-4cdb-af65-9e1f4cea69dc)](https://codebeat.co/projects/github-com-emenegro-bookshelf-server-master) [![Build Status](https://travis-ci.org/emenegro/bookshelf-server.svg?branch=master)](https://travis-ci.org/emenegro/bookshelf-server)

Example app to learn Node.js and MongoDB. A very simple REST API to manage a bookshelf.

## Authentication

In this first version there is no authentication so in order to allow several users to store their bookshelf each request has to be run passing a HTTP header named **`uuid`** of type `String`. The value passed to this header is irrelevant as long as it is always the same; for example, in a mobile app this value could be the device id.

Each database registry is stored with the UUID passed when creating it, and it will be compared with the provided one when an operation is performed.

**NOTE**: this is an exercise, not a production-ready code, please **don't** use this kind of approach in your production code.

## Endpoints

* [GET search](#search)
* [GET books](#list-books)
* [POST books](#create-book)
* [GET books/[id]](#get-book)
* [PUT books/[id]](#update-book)
* [DELETE books/[id]](#delete-book)

### Search
Executes a search against Google Books API and returns the results.

```sh
curl -X GET "http://127.0.0.1:8080/search?q=[QUERY]" \
     -H "uuid: 0000-1111-2222-3333-4444" \
     -H "Content-Type: text/plain"
```

### List books
Lists all the books in the user's collection.

```sh
curl -X GET "http://127.0.0.1:8080/books" \
     -H "uuid: 0000-1111-2222-3333-4444" \
     -H "Content-Type: text/plain"
```

### Create book
Adds a book to the user's collection. 


```sh
curl -X POST "http://127.0.0.1:8080/books" \
     -H "uuid: 0000-1111-2222-3333-4444" \
     -H "Content-Type: application/json" \
     --data-raw "$JSON_BODY"
```

### Get book
Gets a book from the user's collection.

```sh
curl -X GET "http://127.0.0.1:8080/books/[BOOK_ID]" \
     -H "uuid: 0000-1111-2222-3333-4444"
```

### Update book
Updates a book of the user's collection. Used to mark `isRead` flag.

```sh
curl -X PUT "http://127.0.0.1:8080/books/[BOOK_ID]" \
     -H "uuid: 0000-1111-2222-3333-4444" \
     -H "Content-Type: application/json" \
     --data-raw "$JSON_BODY"
```

### Delete book
Deletes a book from the user's collection.

```sh
curl -X DELETE "http://127.0.0.1:8080/books/[BOOK_ID]" \
     -H "uuid: 0000-1111-2222-3333-4444" \
     -H "Content-Type: text/plain"
```

## Installation

Use **docker-compose** in order to install the whole app and its dependencies.

Run `docker-compose up` in the project's root folder and, if everything is OK you could test the API in `http://127.0.0.1:8080`.

Inside `etc/` folder there are both [Paw](https://paw.cloud) and [Postman](https://www.getpostman.com) collections with some prefilled data to play with.

## ToDo

* Add proper user authentication to get rid of UUID header.
