# s15_Moore_data_lecture_notes
##Notes for Data Engineering

###January 15
####Continuing on Servers
* __get__, __post__, put, and delete  <-- html methods
  * Extra care with put and delete, as this can be a security threat
* htmls with images can send out hundreds of requests
  * Plenty of ways an html can send out numbers of requests that add additional time
  * Successful websites can keep their waiting under 2 seconds
* Each content block on a page can be a call to a web service
  * advertisements are calculated individually on a click to request things from a server

How do I write a simple web service? 

__REST__ 
Representation - resources available on web. Referenced by URIs <-- URL

__CRUD__
Create. Read. Update. Destroy.

/users/{id}
Get Users - Read - get representation of all users
Post Users - Create {data}
Put - Update 
Delete - Destroy

/search?{attribute-value pairs}

###January 20
####Rest
* Architectuaral style for web services (by Roy Fielding) 
  *Rest is an appriach to developing web services that mimics the design of the Web itself
  * For each resources you can perform operations on it similar to the main operations of the HTTP Specs. 
* Each resource can perform at least one of the following CRUD (create, read, update, delete) operations:
  * Post --> Create
    Get --> read
    Put --> Update
    Delete --> Delete

Example: 
  - GET /api/1.0/users (retrieves list of users) 
  - GET /api/1.0/users (retrieve details of user 0)
  - POST /api/1.0/users (create a new user) 
  - DELETE /api/1.0/users/0 (Delete user 0) 
  - GET /api/1.0/search?q=__tattersail__ (perform a search with the query __tattersail__)

#####Discussion
*Each operation may preduce a result
*Post and Put methods typically send data
  * Other formats are possible: HTML and XML (as opposed to JSON)
* If request needs to be authenticated -- authentication data appears in HTTP headers

  - GET /api/1.0/posts/0/comments/1 (Get the first comment on post 0)
  - POST /api/1.0/posts/0/comments  (Create a new comment on post 0)

#####Issues
__Security__: How do you authenticate users?
__Identity__: How are IDs assigned to resources?
__Failure__: How do we handle failure situations?
__Persistence__: How are resources stored?

###January 27 Notes
Lecture consisted of Instructor providing examples of code. 

###January 29 Notes
#####Looking at Express
* Express: Web app framework 
  * Written in Javascript for use in Node.js
* Makes easy to define endpoints of your web-based service.
* Has features that allow to create website
* Express is minimal framework. Augmented by node packages
  * Wired in as Middleware

__Example of web servece in Express__

###February 2 Notes
#####AngularJS
* web-application framework written for Javascript
  * implementation of model-view-controller in web browser
    * easier to produce web clients 
* Data bindings
  * value of HTML tag associated with modal object
    * when one changes, Angular updates other automatically
* Controller 
  * Define all state and methods accessed within section of page
  * Can modularize web application and decompose data into small manageable chunks
* Services 
  * controllers come and go from page to page
  * Service maintains state between invocations
    * remain in place for the life of the application
* Directive
  * allow angular to integrate into HTML 
    * can create reusable components that combine controller, data, and HTML
* Injectable 
  * Angular controller and services declare their dependences up front
  * locate at run time and inject them into component that needs them
* Modules
  * primary way of packaging up a set of controllers into Angular application

__Example code from teacher for rest of class__ 

###Notes from February 10
#####Basic idea of requireJS
* Load single javascript file: RequireJS
* Point RequireJS at main.js
  * all files loaded by RequireJS are loaded in parallel, executed in order of dependencies
* Code is MUCH cleaner 

#####IIFES
* immediately invoked function expression

#####Getting Data from Twitter
__Make an account on twitter__ 
__dev.twitter.com__
__manage your apps__

###Notes for February 17

#####Twitter Data Collection Framework
* High Level of framework 
  * Core <-- Request <-- Helpers 
    v
* Standardized Constructor
  * Expects an args hash with up to 3 entries: 
    * params, data, and log
  * sets the contract required by all sub-classes
* Contracts 
  * Interfaces used in statically-typed languages
  * Improvise in dynamically-typed languages 
    * if a subclass fails to implement on of these methods: __BOOM__
  * TwitterRequest has public collect method that yields collected data to the caller
  * Subclasses __must__ provide implementations of
    * url, request_name, twitter_endpoint, and success
  * __may__ provide implementations of: 
    * error, authorization, options, make_request, and collect
  * Params and Props
    * two new features in Params helper:
      * control if parameter is included in request
      * display parameters being sent with a request
  * Rates helper invokes a twitter endpoint to get the apps current set of rate limits
    * these rates are stored in a class variable so they are shared across all TwitterRequest instances created by an app
    * These global rates are only refreshed when needed
  * Types of requests:
    * MaxIdRequest
      * subclass for endpoints that need to traverse timelines with max_id param
      * defines new construct of:
        * init_condition, condition, and update_condition
    * CursorRequest 
      * similar to Max ID request
      * However, doesn't need to define contract for subclasses
      * can implement all of required functionality directly 
