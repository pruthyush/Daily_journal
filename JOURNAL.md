# Daily journal of a Student to Professional
##### ***why a journal? - When I was OTW to home I felt stuck like Im not reaching my destination and I was so impatient to reach the destination but at the end I reached then I got this thought of everything takes time and patience so this is for me to enjoy the journey that I can look back at a certain point and say "what level have I reached"***
This is a daily journal that kept updating in my masters program . What I learned and what I experienced are recorded here.
## Day 0 - Preparation [core]- 1 Mar
- Access control vulnerabilities
- Authentication vulnerabilities
- SQL injection
- Cross-site scripting (XSS)
- Cross-site request forgery (CSRF)
- Business logic vulnerabilities
- Information disclosure
  
## Day 1 - Access control vulnerabilities and privilege escalation - 1 Mar

### what is access control

Access control is the application of constraints on who or what is authorized to perform actions or access resources. In the context of web applications, access control is dependent on authentication and session management:

- Authentication - confirms that the user is who they say they are.
- Session management - identifies which subsequent HTTP requests are being made by that same user.
- Access control - determines whether the user is allowed to carry out the action that they are attempting to perform.

## Day 2 - Examples of vertical Previlege escalation - 2 Mar

vertical Previlege escalation - If a user can gain access to functionality that they are not permitted to access then this is vertical privilege escalation(VPE).

For example, if a non-administrative user can gain access to an admin page where they can delete user accounts, then this is vertical privilege escalation

happens when the application doesnt enforces protection for sensitive functionality

ie administrative functions might be linked from an administrator's welcome page but not from a user's welcome page. However, a user might be able to access the administrative functions by browsing to the relevant admin URL.

### Lab - 1 : Unprotected Admin functionality
Aim : delete a/c carlos

lab status : Done

editing URL and entering any admin page is called : security by obscurity

## Day 3 - Lab - 2 : Unprotected admin functionality with unpredictable URL - 3 Mar

Aim: Delete a/c Carlos

lab status: Done

## Day 4 - Parameter-based access control methods - 4 Mar

Some applications determine the user's access rights or role at login, and then store this information in a user-controllable location. This could be:

1. A hidden field.
2. A cookie.
3. A preset query string parameter.

The application makes access control decisions based on the submitted value.

eg:- https://insecure-website.com/login/home.jsp?admin=true 
     https://insecure-website.com/login/home.jsp?role=1

Lab - 3 : User role controlled by request parameter

Aim: access the admin panel and using it to delete the user carlos. 

Hint: You can log in to your own account using the following credentials: wiener:peter

lab status: Pending

## Day 5 - Completing Lab with Burpe Suite and continue academy

Installed burp suite

## Day 6 - Due to Lack of knowledge starting from the fundamentals

### 1. HTTP fndms - type in browser > browser send "req" > server sends "resp"

Browsr => Req  |  Server => Resp

BASIC WORKING OF REQ AND RESP WHEN LOADING A WEB

Browsr Req:       GET /product HTTP/1.1 | Host: `example.com`

Server Resp:      HTTP/1.1 200 OK | Content-Type: text/html

Webpage Loads

### 2. Structure of HTTP Req (3 main parts)

1. Request line : "Give me this page"

   "GET /login HTTP/1.1" | This contains : Method → "GET" ,Path → "/login", Protocol → "HTTP/1.1"

2.Header : Gives extra information to server

  Host: example.com | User-Agent: Chrome | Cookie: session=abc123

  Host → which website is needed | User-Agent → type of browser using | Cookie → login session data

3. Req Body : Used mainly in POST Req

   username=admin&password=123

   Use cases are Login forms, File uploads , Search Queries

### 3. HTTP Meathods : Tells server what action to perform

**GET** : Used to retrieve data 
  
  Eg : "GET /profile" - translates to :get me the profile page
       
  *`/product?id=10` - get request always have some parameters in the URL*
  
**POST** : used to send data to the server

  Eg : "POST /login" | data send in body - "username=admin password=123"

**PUT** : Used to update the existing data

  Eg : "PUT /user/123" , Some api allow file uploads with PUT this is abused by attackers

**DELETE** : Used to delete resources

  Eg : "DELETE /account/123" , If access control is weak attackers may delete other user account

**PATCH** : Used for partially update resources

  Eg : "PATCH /profile" -Chanegs just one field like email

### 4. HTTP Response Structure - Sever sends back to the browsr

EG : "HTTP/1.1 200 OK , Content-Type: text/html"
   
   *Response part (status Line): 'HTTP/1.1 200 OK' 
   Protocol - HTTP/1.1, Status code - 200 , Message - OK*
  
   *Response Headers : 'Content-Type: text/html Set-Cookie: session=xyz' 
   Content-type - File type , Set-Cookie - login session, [extra] Location - redirection*

   *Response Body : Contains the Webpage Contents*
    
  EG: `<html>`
      `<h1>Welcome</h1>`
      `</html>`

### 5. HTTP Status code ***(IMPORTANT)***

**200 - SUCCESS | Request Worked**
  Eg: `HTTP/1.1 200 OK`

**301/302 - Redirect** 
  Eg: `Location: /login`

**403 - Forbidden | Access denied**
  Eg: `Trying to access Admin Pannel`

**404 - Not found | Page doesnt exist**

**500 - Sever Error | Server crashed or misconfigured, Sometimes indiacte vulnuerablities**

### URL Structure

Eg for URL: `https://example.com/product?id=10`

*Protocol - `https`, Domain - `example.com`, Path -`/product`, Paramter - id=10 (Parameters are very important for attcks)*

### 6. Query Parameters

Eg : `/search?q=laptop`

*Parameter - q=laptop | [atkr tries to modify values ie: `q=' OR 1=1` this triggers **SQL injection**]*

### Headers for Security Testing [Imp for Hacking]

**Cookie : Used to maintain login state**

*eg: `Cookie: session=abc123` **[if stolen atckr logs in as victim]***

**Authorization : Used in APIs**

*eg: `Authorization: Bearer token123` **[If stolen atckr access restricted data]***

**Referer : Some Website *Trust* this header incorrectly**

*eg: `Referer: https://example.com/login`

### 7. ***Stateless*** Nature of HTTP

Http is **stateless** means the server does not remeber previous *req*

*eg: `GET /profile`* |  *`GET /settings`* - **Racist Server** [Server treat them seperately] 

*Session and cookies are used to maintain the state*

### 8. Why need of HTTP

Every vul happns in *req* and *resp*

eg : 
- **SQL Injection - manipulates parameters**
- **IDOR[insecure direct object response] - changing IDs**
- **Authenticatn bypass - Modifying login req**
- **CSRF[Cross site req forgery] - abusing POST req**


### ***BURP SUITE BASICS***

#### 1. Burp suite - sec test proxy tool 

**BROWSR** <=> **BURP SUITE** <=> **INTERNET** <=> **SERVER**

- Capture req
- modify them
- send them *again*
- Analyze responses

Instead of brwsr talking directly the traffic passes through Burp this allows us to **Intercept and Manipulate req**

#### 2. CORE CONCEPTS

Every webst snds a req : `GET /profile HTTP/1.1 | Host: example.com | Cookie: session=abc123`

Server resp : `HTTP/1.1 200 OK`

Normally we cannot modify req but Burp we can intercept and chnge anything

eg attk: 
  OG req :`GET /account?id=101` | Mod req : *`GET /account?id=102`* (note : 101 -> 102) 
  If this returns another user data : IDOR Vul

#### 3. **Proxy - Heart of Burp**

Proxy capts traffics from browsr[(In burp suite) PROXY => INTERCEPT ]

when enabled the req are paused before sending them to the server 
  
  eg for captured req:
  `GET /login HTTP/1.1 | Host: site.com | Cookie: session=123`

### 4. Setting up browsr with burp

burp listen on : `127.0.0.1:8080`

## Day 7 Again on burp suite(Portswigger apprentice) - 13 Mar

Due to some mental pressure i havent been myself today i will go for the basic start of the burp suite i e choosing the **apprentice learning path**

Path Traversal(Directory Traversal) -  vulner enable an attacker to read arbitrary files on the server that is running an application this includes:

1. Application code and data
2. Credentials for back-end systems
3. Sensitive operating system files

*`an attacker might be able to write to arbitrary files on the server, allowing them to modify application data or behavior, and ultimately take full control of the server.`*

