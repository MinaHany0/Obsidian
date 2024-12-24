## What is access control?

Access control is the application of <span style="color:rgb(255, 192, 0)">constraints</span> on who or what is authorized to<span style="color:rgb(255, 192, 0)"> perform actions or access resources.</span> In the context of web applications, access control is dependent on <span style="color:rgb(255, 192, 0)">authentication</span> and <span style="color:rgb(255, 192, 0)">session management</span>

- <span style="color:rgb(255, 192, 0)">Authentication**</span> confirms that the user is who they say they are.
- <span style="color:rgb(255, 192, 0)">Session management**</span> identifies which subsequent HTTP requests are being made by that same user.
- <span style="color:rgb(255, 192, 0)">**Access control**</span> d
- 
- etermines whether the user is allowed to carry out the action that they are attempting to perform

<span style="color:rgb(255, 192, 0)">Access Control is vulnerable because decisions are taken by humans</span> 
# Access Control Security Models
## Programmatic access control
With programmatic access control, a<span style="color:rgb(255, 192, 0)"> matrix of user privileges is stored in a database</span> or similar and [access controls](https://portswigger.net/web-security/access-control) are applied<span style="color:rgb(255, 192, 0)"> programmatically</span> with reference to this matrix. This approach to access control can include roles or groups or individual users, collections or workflows of processes and can be highly granular.

## Discretionary access control (DAC)
With discretionary access control, access to resources or functions is <span style="color:rgb(255, 192, 0)">constrained based upon users or named groups of users.</span> Owners of resources or functions have the ability to <span style="color:rgb(255, 192, 0)">assign or delegate access permissions to users</span>. This model is <span style="color:rgb(255, 192, 0)">highly granular </span>with access rights defined to an individual resource or function and user. Consequently the model can become very complex to design and manage.

هنا الmanagers  يقدروا يدوا access  ويتحكمول ولكن فى ال mandatory  محدش يقدر يغير حاجة
## Mandatory access control (MAC)
Mandatory access control is a centrally controlled system of access control in which <span style="color:rgb(255, 192, 0)">access</span> <span style="color:rgb(255, 192, 0)">t</span><span style="color:rgb(255, 192, 0)">o some object (a file or other resource) by a subject is constrained</span>. Significantly, unlike DAC the users and owners of resources have no capability to delegate or modify access rights for their resources. This model is often associated with military clearance-based systems

## Role-based access control (RBAC)
With role-based access control, named roles are defined to <span style="color:rgb(255, 192, 0)">which access privileges are assigned.</span> <span style="color:rgb(255, 192, 0)">Users</span> are then assigned to single or multiple roles. RBAC provides enhanced management over other access control models and if properly designed sufficient granularity to provide manageable access control in complex applications. For example, the purchase clerk might be defined as a role with access permissions for a subset of purchase ledger functionality and resources. As employees leave or join an organization then access control management is simplified to defining or revoking membership of the purchases clerk role.

RBAC is most effective when there are sufficient roles to properly invoke access controls but not so many as to make the model excessively complex and unwieldy to manage.


# Types of Access Control
### <span style="color:rgb(255, 192, 0)">Vertical access controls</span>

Vertical access controls are mechanisms that restrict access to sensitive functionality to specific types of users.

With vertical access controls, different types of users have access to different application functions. <span style="color:rgb(255, 192, 0)">For example, an administrator might be able to modify or delete any user's account, while an ordinary user has no access to these actions</span>. Vertical access controls can be more fine-grained implementations of security models designed to enforce business policies such as separation of duties and least privilege.

### <span style="color:rgb(255, 192, 0)">Horizontal access controls</span>
Horizontal access controls are mechanisms that restrict access to resources to specific users.

With horizontal access controls, different users have access to a subset of resources of the same type. <span style="color:rgb(255, 192, 0)">For example, a banking application will allow a user to view transactions and make payments from their own accounts, but not the accounts of any other user.</span> 

### <span style="color:rgb(255, 192, 0)">Context-dependent access controls</span>
Context-dependent access controls restrict access to functionality and resources based upon the state of the application or the user's interaction with it.

Context-dependent access controls prevent a user performing actions in the wrong order. For example, a<span style="color:rgb(255, 192, 0)"> retail website might prevent users from modifying the contents of their shopping cart after they have made payment.
</span>
## Examples of broken access controls
Broken access control vulnerabilities exist when a user can access resources or perform actions that they are not supposed to be able to.
### Vertical privilege escalation
If a user can gain access to functionality that they are not permitted to access then this is vertical privilege escalation. For example, if a non-administrative user can gain access to an admin page where they can delete user accounts, then this is vertical privilege escalation.

#### Unprotected functionality
At its most basic, vertical privilege escalation arises where an application does not enforce any protection for sensitive functionality. For example, administrative functions might be linked from an administrator's welcome page but not from a user's welcome page. However, a user might be able to access the administrative functions by browsing to the relevant admin URL.

For example, a website might host sensitive functionality at the following URL:
`https://insecure-website.com/admin`

This might be accessible by any user, not only administrative users who have a link to the functionality in their user interface. In some cases, the administrative URL might be disclosed in other locations, such as the <span style="color:rgb(255, 192, 0)">robots.txt</span> file:
`https://insecure-website.com/robots.txt`

Even if the URL isn't disclosed anywhere, an attacker may be able to use a word list to brute-force the location of the sensitive functionality.


continue here
https://portswigger.net/web-security/access-control#unprotected-functionality

some websites use "<span style="color:rgb(255, 192, 0)">security by obscurity</span>" like `https://insecure-website.com/administrator-panel-yb556` but it might get leaked in a JavaScript file that constructs the user interface based on the user's role.

## Parameter-based access control methods

Some applications determine the user's access rights or role at login, and then <span style="color:rgb(255, 192, 0)">store this information in a user-controllable location</span>. This could be:

- A hidden field.
- A cookie.
- A preset query string parameter.

The <span style="color:rgb(255, 192, 0)">application makes access control decisions based on the submitted value</span>. For example:

`https://insecure-website.com/login/home.jsp?admin=true https://insecure-website.com/login/home.jsp?role=1`

This approach is insecure because a user can modify the value and access functionality they're not authorized to, such as administrative functions.


continue at lab 6 : : use role can be modified in user profile

#### Broken access control resulting from platform misconfiguration

Some applications enforce access controls at the platform layer. they do this by restricting access to specific URLs and HTTP methods based on the user's role. For example, an application might configure a rule as follows:

`DENY: POST, /admin/deleteUser, managers`

This rule denies access to the `POST` method on the URL `/admin/deleteUser`, for users in the managers group. Various things can go wrong in this situation, leading to access control bypasses.

Some application frameworks support various non-standard HTTP headers that can be used to override the URL in the original request, such as `X-Original-URL` and `X-Rewrite-URL`. If a website uses rigorous front-end controls to restrict access based on the URL, but the application allows the URL to be overridden via a request header, then it might be possible to bypass the access controls using a request like the following:

`POST / HTTP/1.1 X-Original-URL: /admin/deleteUser ...`

An alternative attack relates to the HTTP method used in the request. The front-end controls described in the previous sections restrict access based on the URL and HTTP method. Some websites tolerate different HTTP request methods when performing an action. If an attacker can use the `GET` (or another) method to perform actions on a restricted URL, they can bypass the access control that is implemented at the platform layer.

#### Broken access control resulting from URL-matching discrepancies

Websites can vary in how strictly they match the path of an incoming request to a defined endpoint. For example, they may tolerate inconsistent capitalization, so a request to `/ADMIN/DELETEUSER` may still be mapped to the `/admin/deleteUser` endpoint. If the access control mechanism is less tolerant, it may treat these as two different endpoints and fail to enforce the correct restrictions as a result.

Similar discrepancies can arise if developers using the Spring framework have enabled the `useSuffixPatternMatch` option. This allows paths with an arbitrary file extension to be mapped to an equivalent endpoint with no file extension. In other words, a request to `/admin/deleteUser.anything` would still match the `/admin/deleteUser` pattern. Prior to Spring 5.3, this option is enabled by default.

On other systems, you may encounter discrepancies in whether `/admin/deleteUser` and `/admin/deleteUser/` are treated as distinct endpoints. In this case, you may be able to bypass access controls by appending a trailing slash to the path.



# Horizontal privilege escalation

Horizontal privilege escalation occurs if a user is able to gain access to resources belonging to another user, instead of their own resources of that type. For example, if an employee can access the records of other employees as well as their own, then this is horizontal privilege escalation.

Horizontal privilege escalation attacks may use similar types of exploit methods to vertical privilege escalation. For example, a user might access their own account page using the following URL:

`https://insecure-website.com/myaccount?id=123`

If an attacker modifies the `id` parameter value to that of another user, they might gain access to another user's account page, and the associated data and functions.

#### Note
<span style="color:rgb(255, 192, 0)">This is an example of an insecure direct object reference (IDOR) vulnerability. This type of vulnerability arises where user-controller parameter values are used to access resources or functions directly.</span> 
ال  Insecure Direct Object Reference هو عبارة عن دخول مباشر لل اوبجكت بدون تاكيد على هوية المستخدم زى ما حصل فوق كدا

LAB

 [User ID controlled by request parameter](https://portswigger.net/web-security/access-control/lab-user-id-controlled-by-request-parameter)

Solved

In some applications, the exploitable parameter does not have a predictable value. For example, instead of an incrementing number, an application might use <span style="color:rgb(255, 192, 0)">globally unique identifiers (GUIDs) to identify users.</span> This may prevent an attacker from guessing or predicting another user's identifier. However, the GUIDs belonging to other users <span style="color:rgb(255, 192, 0)">might be disclosed elsewhere in the application where users are referenced</span>, such as user messages or reviews.

LAB [User ID controlled by request parameter, with unpredictable user IDs](https://portswigger.net/web-security/access-control/lab-user-id-controlled-by-request-parameter-with-unpredictable-user-ids)

Solved

In some cases, an application does detect when the user is not permitted to access the resource, and returns a redirect to the login page. However, the response containing the redirect might still include some sensitive data belonging to the targeted user, so the attack is still successful.

LAB [User ID controlled by request parameter with data leakage in redirect](https://portswigger.net/web-security/access-control/lab-user-id-controlled-by-request-parameter-with-data-leakage-in-redirect)

### Horizontal to vertical privilege escalation

Often, a horizontal privilege escalation attack can be turned into a vertical privilege escalation, by compromising a more privileged user. For example, a horizontal escalation might allow an attacker to reset or capture the password belonging to another user. If the attacker targets an administrative user and compromises their account, then they can gain administrative access and so perform vertical privilege escalation.

An attacker might be able to gain access to another user's account page using the parameter tampering technique already described for horizontal privilege escalation:

`https://insecure-website.com/myaccount?id=456`

If the target user is an application administrator, then the attacker will gain access to an administrative account page. This page might disclose the administrator's password or provide a means of changing it, or might provide direct access to privileged functionality.

LAB [User ID controlled by request parameter with password disclosure](https://portswigger.net/web-security/access-control/lab-user-id-controlled-by-request-parameter-with-password-disclosure)


### Insecure direct object references

Insecure direct object references (IDORs) are a subcategory of access control vulnerabilities. IDORs occur if an application uses user-supplied input to access objects directly and an attacker can modify the input to obtain unauthorized access. It was popularized by its appearance in the OWASP 2007 Top Ten. It's just one example of many implementation mistakes that can provide a means to bypass access controls.

LAB [Insecure direct object references](https://portswigger.net/web-security/access-control/lab-insecure-direct-object-references) 
in this lab, when requesting the chat logs, the server is serving them using static pages
so for example the URL for chat is /chat/2.txt

so if you look for /chat/1.txt we find an old chat between carlos and the bot and it contains the password for carlos and we can log in to\ his account

### Access control vulnerabilities in multi-step processes

Many websites implement important functions over a series of steps. This is common when:

- A variety of inputs or options need to be captured.
- The user needs to review and confirm details before the action is performed.

For example, the administrative function to update user details might involve the following steps:

1. Load the form that contains details for a specific user.
2. Submit the changes.
3. Review the changes and confirm.

Sometimes, a website will implement rigorous access controls over some of these steps, but ignore others. Imagine a website where access controls are correctly applied to the first and second steps, but not to the third step. The website assumes that a user will only reach step 3 if they have already completed the first steps, which are properly controlled. An attacker can gain unauthorized access to the function by skipping the first two steps and directly submitting the request for the third step with the required parameters.

LAB  [Multi-step process with no access control on one step](https://portswigger.net/web-security/access-control/lab-multi-step-process-with-no-access-control-on-one-step)
 in this lab we find a two step process for upgrading a user
 - in the first step the admin sends the action and the user name to be upgraded
 - in the second step the user sends the same data with an extra param : <span style="color:rgb(255, 192, 0)">confirmed = true/false</span> 
 - notice that the cookies and everything is the same from our view prespective
 - but the beck end is only applying checking on the first step 
 - because naturally the user will never get to the second step unless he is familiar with the process like in the lab
 - so when you submit the second step directly <span style="color:rgb(255, 192, 0)">with the confirmed parameter and the normal user cookie</span> you can upgrade the user directly and solve the lab

### Referer-based access control

Some websites base access controls on the `Referer` header submitted in the HTTP request. The `Referer` header can be added to requests by browsers to indicate which page initiated a request.

For example, an application robustly enforces access control over the main administrative page at `/admin`, but for sub-pages such as `/admin/deleteUser` only inspects the `Referer` header. If the `Referer` header contains the main `/admin` URL, then the request is allowed.

In this case, the `Referer` header can be fully controlled by an attacker. This means that they can forge direct requests to sensitive sub-pages by supplying the required `Referer` header, and gain unauthorized access.

LAB  [Referer-based access control](https://portswigger.net/web-security/access-control/lab-referer-based-access-control)

this lab is easy since we know what to do but I learnt something extra
here the authorization over the upgrading or downgrading a user is done using the referrer header
- meaning if the referrer is /admin then this means that the user is authorized.
- however I thought what if we gave the website <span style="color:rgb(255, 192, 0)">any cookie instead of the user wiener</span> it <span style="color:rgb(255, 192, 0)">WILL NOT RESPOND</span> 
- however even though the user wiener is un-authorized, it still can give him permission to do the stuff

NOTICE THAT: most websites will r<span style="color:rgb(255, 192, 0)">efuse the request itself </span>if the <span style="color:rgb(255, 192, 0)">cookie doesn't match</span> with the application <span style="color:rgb(255, 192, 0)">records</span> for an <span style="color:rgb(255, 192, 0)">active session</span>
also even thought the user wiener is un-authorized, he still has some privileges even if not administrator but still some action are allowed for him, where the anon user has no privileges at all

### Location-based access control

Some websites enforce access controls based on the user's geographical location. This can apply, for example, to banking applications or media services where state legislation or business restrictions apply. These access controls can often be circumvented by the use of web proxies, VPNs, or manipulation of client-side geolocation mechanisms.

## How to prevent access control vulnerabilities

Access control vulnerabilities can be prevented by taking a defense-in-depth approach and applying the following principles:

- Never rely on obfuscation التشويش alone for access control.
- Unless a resource is intended to be publicly accessible, deny access by default.
- Wherever possible, use a single application-wide mechanism for enforcing access controls.
- At the code level, make it mandatory for developers to declare the access that is allowed for each resource, and deny access by default.
- Thoroughly audit and test access controls to ensure they work as designed.