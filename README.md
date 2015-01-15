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
