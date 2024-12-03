# Chapter 1
Web applications often require multiple HTTP transactions to complete a task. For example, when a web browser loads a graphics-rich web page, it first fetches the HTML skeleton for the page layout and then makes additional HTTP requests for embedded resources like images, graphics, and applets. These resources may come from different servers, meaning a web page is typically a collection of multiple resources, not just a single one.

An HTTP message consists of three parts
1. Start Line
2. Header Fields
3. Body

Please differentiate between the <span style="color:rgb(255, 192, 0)">HOST</span> and the <span style="color:rgb(255, 192, 0)">LOCAL RESOURCE</span> : www.store.com/index.html, here the store is host and the index.html is the local resource

HTTP is an <span style="color:rgb(255, 192, 0)">application layer protocol</span>. HTTP doesn’t worry about the nitty-gritty details of network communication instead, it leaves the <span style="color:rgb(255, 192, 0)">details of networking to TCP/IP</span>, the popular reliable Internet transport protocol, TCP Provides:
1. Error free data transportation
2. in order delivery
3. Unsegmented data stream (can dribble out data in any size at any time)

Whenever a URL is <span style="color:rgb(255, 192, 0)">missing</span> a port number, you can naturally <span style="color:rgb(255, 192, 0)">assume it is 80</span> 

Steps of a HTTP transaction between a server and a browser
(a) The browser extracts the server’s hostname from the URL.  
(b) The browser converts the server’s hostname into the server’s IP address.  
(c) The browser extracts the port number (if any) from the URL.  
(d) The browser establishes a TCP connection with the web server.  
(e) The browser sends an HTTP request message to the server.  
(f) The server sends an HTTP response back to the browser.  
(g) The connection is closed, and the browser displays the document

Web applications other than server and client
	Proxies  
	HTTP intermediaries that sit between clients and servers  
	Caches  
	HTTP storehouses that keep copies of popular web pages close to clients  
	Gateways  
	Special web servers that connect to other applications  
	Tunnels  
	Special proxies that blindly forward HTTP communications  
	Agents  
	Semi-intelligent web clients that make automated HTTP requests

Proxies are often used for <span style="color:rgb(255, 192, 0)">security</span>, acting as trusted intermediaries through which all  
web traffic flows. Proxies can also<span style="color:rgb(255, 192, 0)"> filter requests and responses</span>; for example, to  
<span style="color:rgb(255, 192, 0)">detect</span> application <span style="color:rgb(255, 192, 0)">viruses</span> in corporate downloads or to<span style="color:rgb(255, 192, 0)"> filter adult content</span> away  
from elementary-school students. We’ll talk about proxies in detail in Chapter 6.

Remember that : web cache or caching procy is a sepcial type of proxy servers


## Tunnels  
Tunnels are HTTP applications that, after setup, <span style="color:rgb(255, 192, 0)">blindly relay raw data between two  
connections</span>. HTTP tunnels are often used to<span style="color:rgb(255, 192, 0)"> transport non-HTTP data over one or  
more HTTP connections</span>, without looking at the data.  
One popular use of HTTP tunnels is to<span style="color:rgb(255, 192, 0)"> carry encrypted Secure Sockets Layer</span> (SSL)  
traffic through an HTTP connection,

## Agents
something making web requests on the user's behalf like web browsers or <span style="color:rgb(255, 192, 0)">machine automated user agents</span> (spiders or web robots) that browse the web automatically for various uses: building web archives for web content


## URL Syntax

`<scheme>://<user>:<password>@<host>:<port>/<path>;<params>?<query>#<frag>

Schemes: What Protocol to Use  
The scheme is really the main identifier of how to access a given resource; it tells the  
application interpreting the URL what protocol it needs to speak. In our simple  
HTTP URL, the scheme is simply “http”.


## Parameters
many protocols require more information to work than the host and path to object.  

Applications interpreting URLs need these <span style="color:rgb(0, 176, 80)">protocol parameters</span> to <span style="color:rgb(0, 176, 80)">access the  
resource</span>. Otherwise, the server on the other side might not service the request or, worse yet, might service it wrong. <span style="color:rgb(0, 176, 80)">For example, take a protocol like FTP</span>, which has two modes of transfer, binary and text. You wouldn’t want your binary image transferred in text mode, because the binary image could be scrambled.

URLs have a params component. This component is just a <span style="color:rgb(0, 176, 80)">list of name/value  
pairs</span> in the URL, <span style="color:rgb(255, 192, 0)">separated from the rest of the URL (and from each other)</span> <span style="color:rgb(0, 176, 80)">by “;” characters</span>. They provide applications with any additional information that they need to access the resource. For example:  
`ftp://prep.ai.mit.edu/pub/gnu;type=d
there is one param, <span style="color:rgb(0, 176, 80)">type=d</span>, where the name of the param is “type”  
and its value is “d”.


<span style="color:rgb(255, 192, 0)">Remember the difference between URL parameters and Query Strings</span>: 
- Params have <span style="color:rgb(255, 192, 0)">;</span> but query strings have the <span style="color:rgb(255, 192, 0)">?</span> 
- both contain key value pairs
- URL params can appear at the `form-data` but the query strings must always be in the URL

## Query Strings  
Some resources, such as database services, can be asked questions or queries <span style="color:rgb(0, 176, 80)">to narrow down the type of resource being requested.</span> 
everything to the right of the <span style="color:rgb(0, 176, 80)">question mark (?).</span> This is called the query component.![[Book-The Definitive Guide of HTTP-20241122210614951.webp]]

There is no requirement for the format of the query component, except that some characters are illegal
`http://www.joes-hardware.com/inventory-check.cgi?item=12731&color=blue&size=large  
`item=12731&color=blue&size=large  
query string are a series of “name=value” pairs, separated  by “&” characters:  
`http://www.joes-hardware.com/inventory-check.cgi?item=12731&color=blue  

## Fragments
A fragment dangles off the right-hand side of a URL, preceded by a # character. For example:  
`http://www.joes-hardware.com/tools.html#drills

Because HTTP servers generally deal only <span style="color:rgb(0, 176, 80)">with entire objects</span>, not with fragments of objects, clients don’t pass fragments along to servers. After<span style="color:rgb(0, 176, 80)"> your browser </span>gets the entire resource from the server, it then uses the fragment to display the <span style="color:rgb(0, 176, 80)">part of the resource</span> in which you are interested.

## Expandomatic URLs

Hostname expansion  
In hostname expansion, the browser can often expand the hostname you type in into the full hostname without your help, just by using some simple heuristics. For example if you type “yahoo” in the address box, your browser can automatically insert “www.” and “.com” onto the hostname, creating “www.yahoo.com”.

History expansion  
Another technique that browsers use to save you time typing URLs is to store a  
history of the URLs that you have visited in the past

<span style="color:rgb(0, 176, 80)">Be aware that URL auto-expansion may behave differently when used with proxies.  
We discuss this further in “URI Client Auto-Expansion and Hostname Resolution”</span> 

## The URL Character set
- consists of A-Z capital and lower and 0-9 and some chars (like `-`, `_`, `.`, `~`).
- other character are not transmitted and have special meaning in URL context like (#,&, ?)
- URL encoding came to enable the transmission of these special characters without confusion by encoding them using the <span style="color:rgb(255, 192, 0)">%</span> character which is <span style="color:rgb(255, 192, 0)">followed by the hexadecimal representation of asci code</span> 
- '#' is 23, & is 26, % itself is 25 and so on.
- ( ) space character is %20 , while Tilda ~ is %7E

## Character Restrictions
some chars have been reserved to have special meaning in URL context


| <span style="color:rgb(255, 192, 0)">Character</span> | <span style="color:rgb(255, 192, 0)">Reservation/Restriction  </span><br><br>                                                                                                                   |
| ----------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| %                                                     | Reserved as escape token for encoded characters                                                                                                                                                 |
| /                                                     | reserved for delimiting splitting up paths in path component                                                                                                                                    |
| .                                                     | reserved in the path component                                                                                                                                                                  |
| ..                                                    | reserved in the path component                                                                                                                                                                  |
| '#'                                                   | reserved as the fragment delimiter                                                                                                                                                              |
| ?                                                     | reserved as the query string delimiter                                                                                                                                                          |
| ;                                                     | reserved as the params delimiter                                                                                                                                                                |
| :                                                     | reserved to delimti the scheme, user password, and host/port components                                                                                                                         |
| $ , +                                                 | reserved                                                                                                                                                                                        |
| @&=                                                   | reserved because they have special meaning in some schemes                                                                                                                                      |
| {} \| ^ ~ [] '                                        | <span style="color:rgb(255, 192, 0)">restricted</span> because of unsafe handling by transport agents such as gateways                                                                          |
| <> "                                                  | Unsafe; should be encoded because these characters often have meaning outside the scope of the URL,  <br>such as delimiting the URL itself in a document (e.g., “http://www.joes-hardware.com”) |
| 0x00–0x1F, 0x7F                                       | <span style="color:rgb(255, 192, 0)">Restricted</span>, because these chars fall within the non printable section of the US-ASCI Character set                                                  |
| > 0X7F                                                | <span style="color:rgb(255, 192, 0)">restricted</span>; these characters fall outside the 7-bit range of ASCI Set                                                                               |
<span style="color:rgb(255, 192, 0)">Notice</span> 
Sometimes, <span style="color:rgb(255, 192, 0)">malicious folks encode extra character</span>s in an attempt to get around  applications that are doing pattern matching on URL.
for example, web filtering applications. Encoding safe URL components can cause pattern-matching applications to fail to recognize the patterns for which they are searching. In general, applications interpreting URLs must decode the URLs before processing them.

## Sea of Schemes
- https is same as HTTP except HTTP uses <span style="color:rgb(255, 192, 0)">port 80 </span>by default while HTTPS uses <span style="color:rgb(255, 192, 0)">port 443 default and uses Netscape Secure sockets layer (SSL)</span> , the syntax is identical between HTTP and HTTPS
- <span style="color:rgb(255, 192, 0)">mailto</span> scheme: |Mailto URLs refer to email addresses. Because email behaves differently from other schemes (it does not refer to  <br>objects that can be accessed directly)
  
  Basic Form of mailto: `mailto:<RFC-822-addr-spec>` 
  example: `mailto:joe@joes-hardware.com`

other schemes are there like: ftp, telnet, rstp, rstpu, file. news
---> <span style="color:rgb(255, 192, 0)">search for them when needed or come back to page 39</span>


# Chapter 3 HTTP Messages
## The flow of messages

The terms “inbound,” “outbound,” “upstream,” and “downstream” describe message direction.

### Messages Commute Inbound to the Origin Server
Messages travel <span style="color:rgb(255, 192, 0)">inbound to the origin server</span> and when their work is done they travel <span style="color:rgb(255, 192, 0)">outbound back to the user agent</span> 

HTTP messages always flow downstream like rivers, so the client is upstream of the server for the request but downstream in terms of the response

| Overall range  <br>100-199 | Defined range  <br>100-101 | Category <br>Informational |
| -------------------------- | -------------------------- | -------------------------- |
| 200-299                    | 200-206                    | Successful                 |
| 300-399                    | 300-305                    | Redirection                |
| 400-499                    | 400-415                    | Client error               |
| 500-599                    | 500-505                    | Server error               |

## Methods
- note that not all methods are implemented by every server, a server needs to implements only the GET and HEAD methods for its resources
- even when all the methods are implemented, they have restricted usage, like the DELETE or PUT methods for example
- <span style="color:rgb(255, 192, 0)">GET is the most common methods, HTTP/1.1 requires servers to implement this method</span> 
- <span style="color:rgb(255, 192, 0)">Server developer must ensure</span> that the headers returned by the HEAD method is the same as the GET methods
- الكلام دا معناه ان الserver developer هما بيطبقوا الmethods ينفسهم
- the PUT method is used for the <span style="color:rgb(255, 192, 0)">server</span> to take the <span style="color:rgb(255, 192, 0)">body</span> of the request and <span style="color:rgb(255, 192, 0)">use it to create a new document or if existing to replace it</span> 
	- since <span style="color:rgb(255, 192, 0)">PUT changes</span> in the content, many <span style="color:rgb(255, 192, 0)">servers</span> requires a <span style="color:rgb(255, 192, 0)">password</span> before you can perform a <span style="color:rgb(255, 192, 0)">PUT</span> 
## Extension Methods
HTTP was designed to be <span style="color:rgb(255, 192, 0)">field extensible</span> , extension methods are nay methods that were not defined in the HTTP/1.1 standard
- example of them are some that are defined in the <span style="color:rgb(255, 192, 0)">webDAV HTTP extension</span> like
	1. LOCK: allows a user to lock the resource to not be edited by another person at the same time
	2. MKCOL: allows a user to create a resource
	3. COPY: facilitates copying resources on a server
	4. moves a resource on a server
Proxies should try to <span style="color:rgb(255, 192, 0)">relay messages with unknown methods </span>downstream <span style="color:rgb(255, 192, 0)">without</span> breaking the<span style="color:rgb(255, 192, 0)"> end to end behavior </span>
- otherwise they should respond with a <span style="color:rgb(255, 192, 0)">501 "Not implemented status code"</span> 

