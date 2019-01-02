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

AJAX stands for **Asynchronous JavaScript and XML**. When developing on the web,
Asynchronous JavaScript allows us to set aside a piece of logic to be processed later on. Feel free to learn more about how that works [here](https://blog.hellojs.org/asynchronous-javascript-from-callback-hell-to-async-and-await-9b9ceb63c8e8) but mainly AJAX is going to be used for updating parts of the webpage without having to reload the whole page.

## Creating an Event 

The first step of creating an AJAX call is to create an *event listener function*. 
The browser receives events from the operating system every time something happens. The event listener function will be executed when the whenever the browser receives that event. Each DOM element can have its own set of event listeners. 

```
$(() => {
  // use jQuery to target the html form by ID
  $('#getAllBooksForm').on('submit', events.onGetAllBooks)
  $('#getOneBookForm').on('submit', events.onGetOneBook)
})
```
Here two event listeners are attached to a respective ```form``` element inside the DOM.

## Handling the Event 

Next, we define the event handling function. The form element used for our example has a default action of refreshing the webpage so we use the event's ```preventDefault()``` method. While we are here we can traverse the DOM to get neccessary data for our request.

Now we can call the fuction which will encapsulate our request with any useful data as a an arguement *(even if we haven't defined it just quite yet)*

Using jQuery means our request object is defined as a deferred obeject which gives us access to the ```then``` and ```catch``` methods to handle the API response.


```
const onGetOneBook = function (event) {
  // prevent default reload of page
  console.log('got into onGetOneBook...about to prevent default')
  event.preventDefault()
  
   const input = getFormFields(event.target) // input = { book: { id: 100 } }
  
   api.getOneBookFromApi(input.book.id)
    .then(ui.handleOneSuccessResponse)
    .catch(ui.handleFailureResponse)
}
```


**Finally** we can create our AJAX request!

In this example the ```id``` data from the form is being passed into our getOneBook fuction. 

```
const getOneBookFromApi = function (id) {
  return $.ajax({
    url: baseUrl + `/books/${id}`,
    method: 'GET'
  })
}
```

This fuction returns the output of jQuery's ```ajax()``` method, whenever that is evaluated.

The $.ajax method has a url parameter as well as an optional ```options``` parameter containing an object literal of the configurations of the AJAX call.