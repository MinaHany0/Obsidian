# understanding the # character

- the <span style="color:rgb(255, 192, 0)">hash</span> character is used as a <span style="color:rgb(255, 192, 0)">fragment identifier</span> meaning:
  when you have a page with multiple sections as careers, about, contact us , it can be used to go directly to this section. for example : `https://en.wikipedia.org/wiki/JavaScript#History` : it will take you directly to the "History" section of the article.

- the hash character is decoded in multiple ways according to its encoding
	1. if normal in the URL, then it will be used by the browser to go the specific section after getting the response from the web server
	2. if it is <span style="color:rgb(255, 192, 0)">URL-decoded</span> as in <span style="color:rgb(255, 192, 0)">%23 (its hexadecimal ASCI encoding)</span> , the browser will skip the section part and start sending it to the web server <span style="color:rgb(255, 192, 0)">BUT</span> in 2 steps
		1. When the browser sends a request to a server, it follows a specific protocol:
		   - The browser sends the entire URL to the server as is, including any encoded characters.
		   - When it encounters `%23`, it recognizes this as the URL-encoded version of `#` and decodes it before sending the request.
	3. when it reaches the server it will be treated by the **<span style="color:rgb(255, 192, 0)">Server-Side Interpretation</span>**:
		- When the server receives the request, it processes the query string. Here’s how it interprets the incoming request:
		- The server uses libraries or frameworks that automatically handle URL decoding.
		- When the server sees `name=peter%23foo`, it decodes `%23` back into `#`, so the server processes the parameter as `name=peter#foo`

# Understanding the effect of the # char

You can use a URL-encoded `#` character to attempt to truncate the server-side request. To help you interpret the response, you could also add a string after the `#` character.

For example, you could modify the query string to the following:
`GET /userSearch?name=peter%23foo&back=/home`

The front-end will try to access the following URL:
`GET /users/search?name=peter#foo&publicProfile=true`

## <span style="color:rgb(255, 192, 0)">Note</span>

<span style="color:rgb(255, 192, 0)">It's essential that you URL-encode the `#` character. Otherwise the front-end application will interpret it as a fragment identifier and it won't be passed to the internal API</span> 

- now the site above you will truncate the public profile = true param from the backend API
- this maybe useful in exploiting the bad querying the developer used because you maybe able to give yourself authorized privileges.

<span style="color:rgb(255, 192, 0)">THEN
</span>
Review the response for clues about whether the query has been truncated. For example, if the response returns the user `peter`, <span style="color:rgb(255, 192, 0)">the server-side query may have been truncated</span>. If an `Invalid name` error message is returned, the application may have treated `foo` as part of the username. This suggests that the server-side request <span style="color:rgb(255, 192, 0)">may not have been truncated.</span>

If you're able to truncate the server-side request, this removes the requirement for the `publicProfile` field to be set to true. You may be able to exploit this to return non-public user profiles.


# Injecting invalid parameters

You can use <span style="color:rgb(255, 192, 0)">an URL-encoded `&` character to attempt to add a second parameter</span> to the server-side request.
For example, you could modify the query string to the following:
`GET /userSearch?name=peter%26foo=xyz&back=/home`

This results in the following server-side request to the internal API:
`GET /users/search?name=peter&foo=xyz&publicProfile=true`

Review the response for clues about how the additional parameter is parsed. For example, if the <span style="color:rgb(255, 192, 0)">response is unchanged this may indicate that the parameter was successfully injected</span> but ignored by the application.

To build up a more complete picture, you'll need to test further.

## Injecting valid parameters

If you're able to modify the query string, you can then attempt to add a second valid parameter to the server-side request.

<span style="color:rgb(255, 192, 0)">you could use the section where we talked about hidden parameters for this </span>
For example, if you've identified the `email` parameter, you could add it to the query string as follows:
`GET /userSearch?name=peter%26email=foo&back=/home`

This results in the following server-side request to the internal API:
`GET /users/search?name=peter&email=foo&publicProfile=true`

Review the response for clues about how the additional parameter is parsed.


you could refer to this video for more explanation if you forget [HTTP Parameter Pollution Explained](https://www.youtube.com/watch?v=QVZBl8yxVX0)
if we have this query : `/details/?user=Anderson&user=Smith`
<span style="color:rgb(255, 192, 0)">which one will be in the result ?</span>
- the answer is according the backend technology used in the server code, if the technology is 
	- JSP + Apache Tomcat or NodeJS / express-> the result will contain the first param only
	- PHP + Apache -> the result will contain the second param only
	- ASP.NET +  IIS -> the result will contain both params concatenated
- this was due to the <span style="color:rgb(255, 192, 0)">lack of an RFC for parsing the query</span> parameters

<span style="color:green">NOTICE THAT THIS IS ALSO ALL BECAUSE THE PARAMETERS THEMSELVES ARE NOT ENCODED</span> 
- a great example is a bank which when doing a transfer has the query
	`Amount=1000&to=mina`
- the backend receives these params and uses the cookie from the browser to identify the sender
	- so the backend API will have the params `from=andrew&Amount=1000&to=mina`
- the attacker can exploit this request if the technology used is PHP+ apache into putting 2 params at the back 
	- his request before adjustment will look like `from=attacker&Amount=1000&to=mina`
	- his request after adjustment will look like `from=attacker&Amount=1000&to=mina&from=andrew&to=attacker`
- now he has successfully overridden the two params , <span style="color:rgb(255, 192, 0)">the FROM and the TO</span> 

<span style="color:rgb(255, 192, 0)">If you're able to override the original parameter, you may be able to conduct an exploit. For example, you could add `name=administrator` to the request. This may enable you to log in as the administrator user.</span> 

# Testing for server-side parameter pollution in REST paths
A RESTful API may place<span style="color:rgb(255, 192, 0)"> parameter names and values in the URL path</span>, rather than the query string. For example, consider the following path:
`/api/users/123`

The URL path might be broken down as follows:
- `/api` is the root API endpoint.
- `/users` represents a resource, in this case `users`.
- `/123`represents a parameter, here an identifier for the specific user.

Consider an application that enables you to edit user profiles based on their username. Requests are sent to the following endpoint:
`GET /edit_profile.php?name=peter`

This results in the following server-side request:
`GET /api/private/users/peter`

An attacker may be able to <span style="color:rgb(255, 192, 0)">manipulate server-side URL path parameters</span> to exploit the API. To test for this vulnerability, <span style="color:rgb(255, 192, 0)">add path traversal sequences</span> to modify parameters and observe how the application responds.

You could submit URL-<span style="color:rgb(255, 192, 0)">encoded</span> `peter/../admin` as the value of the `name` parameter:
`GET /edit_profile.php?name=peter%2f..%2fadmin`

This may result in the following server-side request:
`GET /api/private/users/peter/../admin`

If the server-side client or back-end API normalize this path, it may be resolved to `/api/private/users/admin`.


# Server-side parameter pollution

Some systems contain <span style="color:rgb(255, 192, 0)">internal APIs</span> that aren't directly accessible from the internet. Server-side parameter pollution occurs when a website embeds <span style="color:rgb(255, 192, 0)">user input in a server-side request</span> to an internal API without adequate encoding. This means that an attacker may be able to manipulate or inject parameters, which may enable them to, for example:

- Override existing parameters.
- Modify the application behavior.
- Access unauthorized data

الفكرة هنا انك عرفت تلعب فى حاجة فى ناحية السيرفر فقط، و المطور مش حاطط فى باله انك شايفها اصلا

To <span style="color:rgb(255, 192, 0)">test</span> for server-side parameter pollution in the query string, place <span style="color:rgb(255, 192, 0)">query syntax characters like `#`, `&`, and `=`</span> in your input and observe how the application responds.

