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

