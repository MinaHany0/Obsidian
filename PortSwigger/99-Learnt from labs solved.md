
# Lab 1
Lesson 1 L the documentation Lab

there are some standard names for the API documentation, which if you discover will help you a lot to find more vulnerabilites

you can crawl an api for the popular names like : swagger, api, openAPI, .....


# Lab 2
lesson 2 : buying a free jacket lab

here we saw that the page displaying the price had a patch method available
- so naturally we tried using it
- its mistake was the authorization
- any user on the website could change the price
- if you were not logged in, then you are "<span style="color:rgb(255, 192, 0)">unauthorized</span>"
- makes no sense really as only some users should have this privilege not anybody on the site

Lesson 3
you need to find more endpoints using intruder to replace the current endpoint with different endpoints based on the nature of the web application (<span style="color:rgb(255, 192, 0)">keywords</span>)

- The <span style="color:rgb(255, 192, 0)">Param miner BApp</span> enables you to automatically guess up to 65,536 param names per request. Param miner automatically guesses names that are relevant to the application, based on information taken from the scope.
- you can use a <span style="color:rgb(255, 192, 0)">content discovery tool</span> to get more hidden endpoints
	- a content discovery tool example applications like : 
		- param Miner (paid through BurpSuite Professiona;)
		- Go Buster: open source and free
		- Dirb: open source and free
		- ffuff: open source and free
	- Many of these application are used for <span style="color:rgb(255, 192, 0)">Brute Forcing</span> 

# Lab 3
try to uncover hidden parameters in requests

try to uncover hidden parameters in URL-Forms and then try to change the hidden parameters, like a <span style="color:rgb(255, 192, 0)">discount</span> parameter, or <span style="color:rgb(255, 192, 0)">isAdmin</span> Parameter


# Lab 4
each website has a robots.txt file which deals with the search engine crawlers and tells them which directories to show in searches and which resources to hide

you can find an unprotected directory in the robots.txt where you can find un-protected features where you can exploit them
lab Link: [Lab: Unprotected admin functionality | Web Security Academy](https://portswigger.net/web-security/access-control/lab-unprotected-admin-functionality)

Lab 5
in this lab we learned to check the cookies for any weird functionality like an admin cookie that is set to true or false.
also I learnt that cookies are persistent so if you change them in inspect application tab , you have its persistent action.
 Lab link: http://burpsuite/show/2/xorv0szlx2h7v3x67sdm2m994ss60ip0
