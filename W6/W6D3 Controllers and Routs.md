>[!Rails mvc Diagram]-
>![[Pasted image 20230628125057.png]]

---

#### The HTTP Request-Response Cycle
![[Pasted image 20230628125213.png]]

---

- When you type `www.google.com` in your url bar and hit `Enter`:
    
    1. Our computer (the client) sends an HTTP request to a server. (GET [www.google.com](http://www.google.com/) page)
    2. The server handles request and formulates an appropriate response.
    3. The HTTP response is sent back to the client.
- HTTP:
    
    - protocol for communication over the internet
    - clients and servers communicate via messages (requests and responses)
    - HTTP requests and responses are just strings
    - HTTP defines how request and response messages are formatted and transmitted

---

## Components of an #HTTP Request

- **Method (HTTP Verb)** (e.g. `GET`, `POST`) - describes what action to perform
- **Path** (e.g. `/users`) - a string that specifies the resource being requested
- **Query String** (e.g. `?loc=new+york` - _optional_) - may further specify the resource requested
- **Body** (e.g. `username=janedoe` - _optional_) - additional data from the client

---

## Anatomy a #URL

The **path** and **query string** are part of the URL

[![url-parts](https://camo.githubusercontent.com/269368b9ccfd302213beb968ec9b06a7357ecd703daa9f9998b5ff6807b25cf8/68747470733a2f2f61612d63682d6c6563747572652d6173736574732e73332e75732d776573742d312e616d617a6f6e6177732e636f6d2f726f757465732d616e642d636f6e74726f6c6c6572732f75726c2d70617274732e706e67)](https://camo.githubusercontent.com/269368b9ccfd302213beb968ec9b06a7357ecd703daa9f9998b5ff6807b25cf8/68747470733a2f2f61612d63682d6c6563747572652d6173736574732e73332e75732d776573742d312e616d617a6f6e6177732e636f6d2f726f757465732d616e642d636f6e74726f6c6c6572732f75726c2d70617274732e706e67)

- The `path` in an http request is simply the path that is relative to the domain.
- We won't worry about the domain for now. We'll focus on the `path` for our discussion of HTTP requests and Rails routes and controllers.

---

## Components of an HTTP Request

- **Method (HTTP Verb)** (e.g. `GET`, `POST`) - describes what action to perform
    
- **Path** (e.g. `/users`) - a string that specifies the resource being requested
    
- **Query String** (e.g. `?loc=new+york` - _optional_) - may further specify the resource requested
    
- **Body** (e.g. `username=janedoe` - _optional_) - additional data from the client
    
- _Note: the path, the query string, and the request body represent the three main ways to send information in an HTTP request_
    

---

## HTTP Methods

- #GET (get something from the database)
- #POST (insert something into the DB)
- #PATCH / #PUT (change something in the DB)
- #DELETE (remove something from the DB)

---

## Components of an HTTP Response

- **Status** (e.g. 200, 302, 404)
    - indicates the type of response (whether successful or not)
    - [Common Response Codes](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes)
- **Body** (e.g. actual HTML document, or data formatted as JSON)
    - the actual data/content the server responded with

---
## Rails #Router
Take in HTTP Requests , decides where to send them

>[!Rails MVC Diagram]-
>![[Pasted image 20230628125057.png]]

- The Router instantiates an **instance of a controller** and invokes an action on that controller

---

## #REST: Representational State Transfer

**REST is a standardized way to interpret an http request and extrapolate the desired response from the server**

#### A convention that maps HTTP verbs onto CRUD actions

- `POST` -------------> **C**reate (insert record into DB)
- `GET` --------------> **R**ead (retrieve record(s) from DB)
- `PATCH` / `PUT` ----> **U**pdate (update record in DB)
- `DELETE` ----------> **D**estroy (remove record from DB)

---

A RESTful API defines a predictable way for us to access and manipulate resources in our application.

- Reminder: #API = Application Programming Interface. (The public-facing portion of our Rails application.)

---
## RESTful Routs

![[Pasted image 20230628125708.png]]

---

## Setting up Routes

- Generate 7 standard RESTful routes for a resource:
    
    ```ruby
    resources :users
    ```
    
- Can add `only` or `except` option to include/exclude certain actions
    
    ```ruby
    resources :users, only: [:create, :destroy]
    ```
    
    ```ruby
    resources :users, except: [:create, :destroy]
    ```
    
- Create a custom route in `routes.rb`:
    
    ```ruby
    get '/users', to: 'users#index'
    ```
    
- Rails Guide on Routing: [https://edgeguides.rubyonrails.org/routing.html](https://edgeguides.rubyonrails.org/routing.html)
    

---

## Example requests to RESTful API

- `GET /users` query all users
- `GET /users/1` query for user with ID 1
- `POST /users` create a new user
- `PATCH /users/1` update user with ID 1
- `DELETE /users/1` delete user with ID 1

Note:

- Here's an example of some requests that would hit our RESTful routes. Note that we've replaced the wildcard `:id` with actual ids.
    - `GET /users` gets the users. `GET /users/1` gets the user with id 1.
- What is the controller action associated with each request?
- For requests with the wildcard, how we will access the `1` inside of our controller action?

---

## #Controllers

 **Takes in HTTP Requests, decides what to _do_ with them & how to respond**

>[!Rails MVC Diagram]-
>![[Pasted image 20230628125057.png]]

- Controllers work with models and views to populate a response to be sent back to the client.

---

## Params

Three ways to pass params in an HTTP request as follows:

- Using _wildcards_ inside a route (e.g. `/users/:id`)
- Via the _query string_ (e.g. `/path?param1=value1&param2=value2`)
- Inside the _request body_ (usually built using a form, basically a bunch of key value pairs)
    - Should avoid for `GET` requests

Note:

- These are three ways you can pass up data with an HTTP request. The body is usually used to pass up data for a `POST` or `PATCH` request, that we want to add or update in our DB. We'll see examples of using each in the demo.

---

## Setting up Controllers

- Be sure to define your class as below:
```ruby
class UsersController < ApplicationController
end
```
Note:
- Write the controllers by hand (avoid using generators)