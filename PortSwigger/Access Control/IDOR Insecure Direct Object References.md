
In this section, we will explain what insecure direct object references (IDOR) are and describe some common vulnerabilities.

## What are insecure direct object references (IDOR)?

Insecure direct object references (IDOR) are a <span style="color:rgb(255, 192, 0)">type of access control vulnerability</span> that arises when an application uses <span style="color:rgb(255, 192, 0)">user-supplied input to access objects directly</span>. The term IDOR was popularized by its appearance in the OWASP 2007 Top Ten. However, it is just one example of many access control implementation mistakes that can lead to access controls being circumvented. IDOR vulnerabilities are <span style="color:rgb(255, 192, 0)">most commonly</span> associated with <span style="color:rgb(255, 192, 0)">horizontal privilege escalation</span>, but they can also arise in relation to <span style="color:rgb(255, 192, 0)">vertical privilege escalation</span>.

## IDOR examples

There are many examples of access control vulnerabilities where user-controlled parameter values are used to access resources or functions directly.

### IDOR vulnerability with direct reference to database objects

Consider a website that uses the following URL to access the customer account page, by retrieving information from the back-end database:

`https://insecure-website.com/customer_account?customer_number=132355`

Here, the customer number is used directly as a record index in queries that are performed on the back-end database. If no other controls are in place, an attacker can simply modify the `customer_number` value, bypassing access controls to view the records of other customers. This is an example of an IDOR vulnerability leading to horizontal privilege escalation.

An attacker might be able to perform horizontal and vertical privilege escalation by altering the user to one with additional privileges while bypassing access controls. Other possibilities include exploiting password leakage or modifying parameters once the attacker has landed in the user's accounts page, for example.

### IDOR vulnerability with direct reference to static files

IDOR vulnerabilities <span style="color:rgb(255, 192, 0)">often arise</span> when sensitive resources are located <span style="color:rgb(255, 192, 0)">in static files</span> on the <span style="color:rgb(255, 192, 0)">server-side filesystem</span>. For example, a website might save chat message t0ranscripts to disk using an incrementing filename, and allow users to retrieve these by visiting a URL like the following:

`https://insecure-website.com/static/12144.txt`

In this situation, an attacker can simply modify the filename to retrieve a transcript created by another user and potentially obtain user credentials and other sensitive data.

LAB  [Insecure direct object references](https://portswigger.net/web-security/access-control/lab-insecure-direct-object-references)  Solved