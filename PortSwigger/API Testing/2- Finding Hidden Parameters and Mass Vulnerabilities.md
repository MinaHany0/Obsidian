# Using Intruder to find hidden endpoints

Once you have identified some initial API endpoints, you can use Intruder to uncover hidden endpoints. For example, consider a scenario where you have identified the following API endpoint for updating user information:

`PUT /api/user/update`

To identify hidden endpoints, you could use Burp Intruder to find other resources with the same structure. For example, you could add a <span style="color:rgb(255, 192, 0)">payload</span> to the `/update` position of the path with a list of other common functions, such as `delete` and `add`.

When looking for hidden endpoints, <span style="color:rgb(255, 192, 0)">use wordlists based on common API naming conventions and industry terms</span>. Make sure you also include terms that are relevant to the application, based on your initial recon.

# Mass assignment vulnerabilities
<span style="color:rgb(255, 192, 0)">Mass assignment</span> known as <span style="color:rgb(255, 192, 0)">auto binding</span> which are used in forms to update data directly by the user can expose hidden parameters and allow users to <span style="color:rgb(255, 192, 0)">change parameters that the developer didn't think will get updates</span>

for example if the user included a role parameter in the payload
```
{
  "name": "John Doe",
  "email": "john@example.com",
  "password": "securepassword",
  "role": "admin"  // This should not be allowed
}
```
if the application accepts the data blindly, this is a privilege vulnerability

<span style="color:rgb(255, 192, 0)">How to prevent this ?</span> 
- whitelist attributes (like allowing only some attributes to be public in a class to be changed by the user, other than them, they must be changed by methods) , example in ruby on rails
```
  class User < ApplicationRecord 
  attr_accessible :name, :email, :password 
  # Only these fields can be mass assigned
```
- using strong parameters in some languages like ruby
- implement Role Based Access Control : where you can change fields only based on roles
- Validation and sanitization of input data
- Review framework documentation on how to handle mass assignment to avoid vulnerabilities

# Identifying hidden parameters

Since mass assignment creates parameters from object fields, you can often identify these hidden parameters by <span style="color:rgb(255, 192, 0)">manually examining objects</span> returned by the API.

For example, consider a `PATCH /api/users/` request, which enables users to update their username and email, and includes the following JSON:
`{ "username": "wiener", "email": "wiener@example.com", }`

A concurrent `GET /api/users/123` request returns the following JSON:
`{ "id": 123, "name": "John Doe", "email": "john@example.com", "isAdmin": "false" }`

This may indicate that the hidden `id` and `isAdmin` parameters are bound to the internal user object, alongside the updated username and email parameters

<span style="color:rgb(255, 192, 0)">after</span> finding the<span style="color:rgb(255, 192, 0)"> hidden parameters</span>, try changing them using the <span style="color:rgb(255, 192, 0)">PATCH</span> request 
- try first putting an invalid value to the  `isAdmin` attribute like `foo` and <span style="color:rgb(255, 192, 0)">observing its behavior to check if it sanitizes the user input</span>
- then try giving it a valid value like <span style="color:rgb(255, 192, 0)">true</span> 

# Preventing vulnerabilities in APIs

When designing APIs, make sure that security is a consideration from the beginning. In particular, make sure that you:

- Secure your documentation if you don't intend your API to be publicly accessible.
- Ensure your documentation is kept up to date so that legitimate testers have full visibility of the API's attack surface.
- Apply an allowlist of permitted HTTP methods.
- Validate that the content type is expected for each request or response.
- Use generic error messages to avoid giving away information that may be useful for an attacker.
- Use protective measures on all versions of your API, not just the current production version.

To prevent mass assignment vulnerabilities, allowlist the properties that can be updated by the user, and blocklist sensitive properties that shouldn't be updated by the user.

