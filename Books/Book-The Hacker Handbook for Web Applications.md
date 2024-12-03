- this shall be a summary for the book, its goal is to have an efficient study and a way to go back and revise the material without actually reading all of the book a second time
- Most of this not will be copy paste of the important stuff and this is OKAY


# Chapter 1 Web Application (in)Security

 - The most serious attacks against web applications are those that expose sensitive data or gain unrestricted access to the back-end systems on which the application is running.
- Application-level denial-of-service attacks can be used to achieve the same results as traditional resource exhaustion attacks against infrastructure. 
- even though most sites use SSL (secure socket layer) in which the exchanged data is encrypted using some cryptography protocol such as RSA but the data is in fact insecure due to some other weakness in the website
	- broken authentication (62%): some defect int he login mechanism
	- Broken access Controls (71%) : this is where the application fails to protect the access to its data, where the attacker can see vulnerable data of users
	- SQL Injection (32%) this is the case where the attacker can inject data into the program database and retrieve or mess with the data 
	- Cross site scripting (94%): this enables the attacker to target other users of the application, potentially gaining access to their data performing unauthorized access on their behalf, or carrying out other attacks against them
	- Information Leakage(78%) this is where the application leaks data when doing incorrect error handling for example
	- cross site request forgery: this flaw means that application users can be induced to perform some malicious actions using their privileges. this vulnerability allows a malicious website visited by the victim user to interact with the application to perform actions that the user did not intend
- <span style="color:rgb(255, 192, 0)">SSL is an excellent technology that protects the communication, but it doesn't defend against the attacks against the client or the server itself like the attacks mentioned above</span> 

<span style="color:rgb(112, 48, 160)">THE MAIN PROBLEM</span> 
 - users can change the HHTP parameters of the request
 - users can send data in un arranged order and may violate any rule put by the developer in the design phase
 - users are not limited to using browsers, many tools exist that allow accessing the webserver but makes requests that no browser normally asks for
- If a vulnerability exists within a web application, an attacker on the public Internet may be able to compromise the organization’s core back-end systems solely by submitting crafted data from his web browser. This data sails past all the organization’s network defenses, in the same way as does ordinary, benign traffic to the web application


two ways the security parameter have moved to the application side
1. the attacker might attack the user data using a vulnerable web application
2. the attacker might attack the company data (in a trusted LAN) using a trusted user application by  utilizing his vulnerable web application.


# Chapter 2: Core Defense Mechanisms

defense mechanisms employed by web applications comprise the following core elements
1. handling user access to the application's data and functionality to prevent users from gaining unauthorized access
2. handling user input to the application's functions to prevent unwanted input from making undesirable behavior
3. handling attackers to ensure the application behaves appropriately when being directly targeted, taking suitable defensive mechanisms to frustrate the attacker







# Chapter 3 : Web application technologies

## The Java Platform

- this java platform presents a software developing tool that abstracts the user abstraction and architecture layering and so much more
it has 
1. Enterprise Java Bean (EJB)
	- EJBs are heavyweight components that encapsulate business logic. They handle complex tasks such as transaction management, security, and concurrency, allowing developers to focus on business functionality rather than low-level concerns.
2. Plain old Java Object : some normal java code that is light weight
3. Java Servlet
4. Java Web Container : a platform or an engine that provides a runtime environment for jaca based web application like Apache Tomcat, BEA WebLogic and JBoss

## ASP.NET

## PHP
Emerged from the project "<span style="color:rgb(255, 192, 0)">personal home page"</span> but it has emerged into a powerful framework for developing web applications

## Ruby on Rails
a framework on which web application can be developed, where it is noticed that it has break necking speed if the developer abided by the rules of it
several vulnerabilities have been found in ruby on rails
- a main vulnerability is the ability to bypass its safe mode analogous to that found in PHP

## SQL : Structured Query Language
## XML : Extensible Markup Language

## Web Services
webs services use Simple Object Access Protocol (SOAP) to exchange data. SOAP typically uses the HTTP protocol to transmit messages and represent the XML format


# Chapter 4 Mapping the Application
1. enumerating the application content
2. understand the technologies being used
3. 