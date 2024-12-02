## What is access control?

Access control is the application of <span style="color:rgb(255, 192, 0)">constraints</span> on who or what is authorized to<span style="color:rgb(255, 192, 0)"> perform actions or access resources.</span> In the context of web applications, access control is dependent on <span style="color:rgb(255, 192, 0)">authentication</span> and <span style="color:rgb(255, 192, 0)">session management</span>

- <span style="color:rgb(255, 192, 0)">Authentication**</span> confirms that the user is who they say they are.
- <span style="color:rgb(255, 192, 0)">Session management**</span> identifies which subsequent HTTP requests are being made by that same user.
- <span style="color:rgb(255, 192, 0)">**Access control**</span> determines whether the user is allowed to carry out the action that they are attempting to perform

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