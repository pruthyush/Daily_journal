# Daily journal of a Student to Professional
###### why a journal - When I was OTW to home I felt stuck like Im not reaching my destination and I was so impatient to reach the destination at the end I reached then I got thisthought everything takes time and patience
This is a daily journal that kept for the portswigger web academy which I started in my masters program . What I learned and what I experienced are recorded here.
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
