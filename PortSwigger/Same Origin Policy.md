video used : [The Same Origin Policy - Hacker History](https://www.youtube.com/watch?v=bSJm8-zJTzQ&ab_channel=LiveOverflow)

continuing this playlist [The History of XSS - YouTube](https://www.youtube.com/playlist?list=PLhixgUqwRTjyakFK7puB3fHVfXMinqMSi)

long before we used to have website written in http with multiple links of other websites which made navigation easier
![[Same Origin Policy-20241202160112739.webp]]

then came the forms in HTML which was used for banks and other stuff![[Same Origin Policy-20241202160849462.webp]]

then came the cookies to authenticate that the user who is dealing with the website is legit, here's how cookies were described to be used by the documentation![[Same Origin Policy-20241202160949906.webp]]

then came LiveScript (later JavaScript) ![[Same Origin Policy-20241202161111347.webp]] <span style="color:rgb(255, 192, 0)">which allowed scripting inside the HTML documents</span> using the `<script> tag` 

<span style="color:rgb(0, 176, 80)">This changed everythings</span>, the web had now event handlers, you could define objects which react with time, and more and more.
so now the web became <span style="color:rgb(0, 176, 80)">dynamic</span>

the websites before used lots of frames (predecessor of today's iframes)

![[Same Origin Policy-20241202161429250.webp]] here we have <span style="color:rgb(0, 176, 80)">two frames</span> in a HTML document with <span style="color:rgb(0, 176, 80)">different URLs</span>
this is how you can implement a navigation bar in content of a page

![[Same Origin Policy-20241202161545716.webp]] frames were really visible and implemented in the browser itself

and as in the JavaScript Documentation, you could now interact with frames![[Same Origin Policy-20241202161636054.webp]]

<span style="color:rgb(0, 176, 80)">so here is the ISSUE</span>
we have a webpage with two different frames, one is the form for some bank and the other is the attacker website
![[Same Origin Policy-20241202161805680.webp]]
 ![[Same Origin Policy-20241202161836200.webp]]and since the two frames can interact using JavaScript, the attacker URL could steal the credentials from the other frame easily using the following code
![[Same Origin Policy-20241202161945982.webp]]

so if you go to a <span style="color:rgb(0, 176, 80)">malicious</span> website, it could load your banking website in <span style="color:rgb(0, 176, 80)">one frame</span> and then use your <span style="color:rgb(0, 176, 80)">browser stored data</span> to login and then using <span style="color:rgb(0, 176, 80)">frames and JavaScript </span>could steal your <span style="color:rgb(0, 176, 80)">credentials</span> and send them to the attacker.

NOW NETSCAPE DEVELOPERS REALISED THIS ISSUE AND RELEASED A NEW VERSION WITH THE FIX

![[Same Origin Policy-20241202162437411.webp]]![[Same Origin Policy-20241202162453967.webp]] now we cannot access the forms data as an array as before or even get the cookie value

this is the fix documentation ![[Same Origin Policy-20241202162643266.webp]]

they prevented also the access of script to listing of local file on the PC![[Same Origin Policy-20241202162852485.webp]]
well we could still access the files but scripts themselves cannot (this not I don't really understand since all code is scripts but ok)


so later this became even more clear when they prevented scripts on one server from accessing properties of documents on another server
![[Same Origin Policy-20241202162837097.webp]] so they invented <span style="color:rgb(0, 176, 80)">Same Origin Policy</span> (SOP)

this was serious issue yes but <span style="color:rgb(0, 176, 80)">there was much more serious vulnerabilities needed to be taken care of </span> 

# Universal XSS
so came before what is now known as "universal XSS", as <span style="color:rgb(0, 176, 80)">we should know</span> XSS is known for <span style="color:rgb(0, 176, 80)">stored XSS</span> and <span style="color:rgb(0, 176, 80)">reflected XSS</span> 

keeping the story short, the same happened to Microsoft explorer with their version of dynamic java called Jscript![[Same Origin Policy-20241202205747386.webp]]

then came some guy named Georgi and reported many many vulnerabilities in IE![[Same Origin Policy-20241202210322012.webp]]
Georgi found another update with IE , with the opening of files inside each other using JavaScript![[Same Origin Policy-20241202211028205.webp]]apparently when opening a file inside another file, the browser keeps the contents of the old file until the second file finishes loading <span style="color:rgb(0, 176, 80)">(-ish :) )  </span> "anyway this is part of the history"

## <span style="color:rgb(0, 176, 80)">Conclusion</span> 
what Georgi and many more security researchers had in common is this , they exploited ways for malicious websites to take use of naive browsers to access more important websites and extract information for the attacker.![[Same Origin Policy-20241202211634540.webp]]
they were able to bypass the 
- cross-frame policy
- cross-frame vulnerability
and that's why it is called <span style="color:rgb(0, 176, 80)">UNIVERSAL</span> because it had nothing to do with the website itself, it was universal across all websites due to the <span style="color:rgb(0, 176, 80)">shortcomings of the browser</span> 



so before XSS (cross site scripting) became known as a thing, this issue was name cross frame vulnerability 
<span style="color:rgb(0, 176, 80)">because</span> what was happening is that a website could embed another website using <span style="color:rgb(0, 176, 80)">iframes</span> or open a new window with another website through JavaScript and by some way could get data from it to the attacker's side![[Same Origin Policy-20241202212721899.webp]]
so the victim's data was <span style="color:rgb(0, 176, 80)">crossing over</span> to the attacker's side

notice that this was starting to become an issue also to emails
as the emails could be opened in the browser and the could read HTML documents and execute JavaScript, so emails was a direct usage of universal XSS and a real danger to many companies.

so developers understood the issue and even talked about <span style="color:rgb(0, 176, 80)">reflected XSS</span>
![[Same Origin Policy-20241202220303999.webp]]
so this is a link that looks like it is going to microsoft but actually it is pointing to another wesbite foo.com with a vulnerable parameter id,
supposedly this parameter id is reflected onto the page.
which loads the malicious script on your website and executes it

<span style="color:rgb(0, 176, 80)">THIS IS WHERE THE NAME CROSS SITE SCRIPTING IS CONFUSING</span> 
because you are injecting a script and not a website

<span style="color:rgb(0, 176, 80)">BUT</span> 
the term was coming from a time when the <span style="color:rgb(255, 192, 0)">issue originated</span> from a <span style="color:rgb(255, 192, 0)">script</span> being loaded from <span style="color:rgb(255, 192, 0)">another website</span> or from <span style="color:rgb(255, 192, 0)">another frame</span> called <span style="color:rgb(0, 176, 80)">cross frame</span> 