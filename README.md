# Connecting Javascript Applications to an Api with AJAX

API's or *Application Programming Interfaces* allow the programs that we write to interact with outside systems by recieving requests and sending responses. 

Ideally, the application within the browser acts as the *client* and talks directly to another application, known as the *server*.

Take a look at the routes of the classic **GA** Books API:

| Verb   | URI Pattern  | Controller#Action |
|:-------|:-------------|:------------------|
| GET    | `/books`     | `books#index`     |
| GET    | `/books/:id` | `books#show`      |
| POST   | `/books`     | `books#create`    |
| PATCH  | `/books/:id` | `books#update`    |
| DELETE | `/books/:id` | `books#destroy`   |


Using this RESTful API our website can make requests to these url's and expect to receive relevant data in return. But wait ...


# What in the World is AJAX ?



