
# Lesson 1
LAB 1 L the documentation Lab

there are some standard names for the API documentation, which if you discover will help you a lot to find more vulnerabilites

you can crawl an api for the popular names like : swagger, api, openAPI, .....


# Lesson 2
Lab2 : buying a free jacket lab

here we saw that the page displaying the price had a patch method available
- so naturally we tried using it
- its mistake was the authorization
- any user on the website could change the price
- if you were not logged in, then you are "<span style="color:rgb(255, 192, 0)">unauthorized</span>"
- makes no sense really as only some users should have this privilege not anybody on the site


# Lesson 3
you need to find more endpoints using intruder to replace the current endpoint with different endpoints based on the nature of the web application (<span style="color:rgb(255, 192, 0)">keywords</span>)

- The <span style="color:rgb(255, 192, 0)">Param miner BApp</span> enables you to automatically guess up to 65,536 param names per request. Param miner automatically guesses names that are relevant to the application, based on information taken from the scope.
- you can use a <span style="color:rgb(255, 192, 0)">content discovery tool</span> to get more hidden endpoints
	- a content discovery tool example applications like : 
		- param Miner (paid through BurpSuite Professiona;)
		- Go Buster: open source and free
		- Dirb: open source and free
		- ffuff: open source and free
	- Many of these application are used for <span style="color:rgb(255, 192, 0)">Brute Forcing</span> 