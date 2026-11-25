# Django Polls App

A small polls app where people can view questions and vote on them. Admins can add and manage questions and choices. Built using the official Django tutorial.

Built for the SUTT Back-End Developer recruitment (Task 1.5).

## How to run

Needs Python 3.10+ and Django 5.2. It uses SQLite, which comes built into Python.

1. `pip install django`
2. `py manage.py migrate`
3. `py manage.py createsuperuser`
4. `py manage.py runserver`, then open http://localhost:8000/polls/


## Extra change
Vote counts can't be negative 

## How the web works

### What happens when you type a URL and hit Enter?
1. The url is parsed and separated into the protocol(http), host(localhost), port(8000), path(/polls/1).
2. External DNS lookup is not needed due to local host and the operating system checks internal host files. TLS verification is
   needed for https protocol.
3. The browser sets up a three way TCP connection to the specific port. It then sends the HTTP request(such as HTML, CSS).
4. The server returns the HTTP response.
5. The browser reads the response and renders the page
   
### What are the client and the server, and how do they talk?
The client is the program which is asking(eg. browser) and the server is the program which is listening and answering. The server 
always responds to the client, never first, over a network using HTTP/HTTPS. A server usually handles multiple clients

### What is HTTP? What's inside a request and a response?
HTTP(Hyper Text Transfer Protocol) is the language for communication between client and server over a network. Each request is made
independently i.e the server does not remember earlier ones.

An HTTP request contains the method(get/post), the path(/polls/1/vote), headers(metadata such as cookies and user agent)

An HTTP response contains the status line(200 OK/404 NOT FOUND), headers(like content type)

### GET vs POST: what's the difference and when to use each?
GET: reads data without changing anything
POST: sends data to change something
GET is used for loading, searching or filtering. POST is used for submitting data such as forms and passwords.

### What do status codes 200, 302, 404 and 500 mean?
200 OK: Success(request worked)
302 FOUND: Redirect(server informs browser to send somewhere else)
404 NOT FOUND: Client error(the url doesnt exist)
500 INTERNAL SERVER ERROR: Server error(backend code crashed due to something like a bug)

### What do HTML, CSS and JavaScript each do?
HTML is responsible for building the website's raw structure such as headings,buttons,links etc.

CSS is responsible for the look of the website such as fonts, borders, images etc.

JS is responsible for making the page responsive such as responding to clicks, updating live counts etc.

### How does a website remember who you are between pages?
The website remembers most commonly by cookies or sessions. A cookie is a piece of data the server asks the browser to store. The 
browser then sends that data in every request. In a session, the server keeps your data in a database. On every request, the browser 
sends a session id, which the server looks up in its database.

### How does a request travel through Django (URLs → views → models → templates)?
1. Request passes through Middleware, which handle sessions and check CSRF tokens
2. Django checks the path against the existing patterns in url.py
3. Django calls the function in view.py which decides what should happen next.
4. The view asks the model, which Django's ORM(Object Relational Mapper) turns into SQL from Python, run it on a database, and give
   back an object.
5. View gives the data to the template, which produces the final webpage
6. The view returns an http response with a status code, which Django sends back to the browser

### Why did the tutorial add {% csrf_token %} to the voting form?
CSRF(Cross Site Request Forgery) token tag adds a hidden token in the HTML form and the browser cookie. When the request is sent, the
middleware checks that the token matches. This prevents any external site from sending a request to the server using your browser's 
session id since browsers dont let one site read another site's pages or cookies which store the csrf token.
