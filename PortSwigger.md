
# API Testing

## <span style="color:rgb(255, 192, 0)">API Documentation:</span> 
a key point in finding out more about an API is the API documentation
- because 2 kinds of people deal with API <span style="color:rgb(255, 192, 0)">(developers and user</span>), there is usually documentation for the developer on how to use this API
- API documentation is o<span style="color:rgb(255, 192, 0)">ften public, especially if the API is intended for use by external developers</span> so you need to review the documentation before you start
- you need to crawl the API to find the documentation, for example: 
	- /api
	- /swagger/index.html
	- /openapi.json
- if you find an endpoint, you need to check its base path for more info

- so what you do is proxy while browsing the website
	- you will find many many URLs and many request
	- you need to check the URLs for any strange URL and then start deep checking them one by one to get any vulnerability from them
## Identifying supported HTTP Methods
you can check supported methods in the intruder section, by highlighting the HTTP verb to be in payload position and add a simple list of HTTP methods so the burp suite can send multiple requests trying each method in the payload position and then check the response for each request

## Identifying supported content types

API endpoints often expect data in a specific format. They may therefore behave differently depending on the content type of the data provided in a request. Changing the content type may enable you to:

- Trigger errors that disclose useful information.
- Bypass flawed defenses.
- Take advantage of differences in processing logic. For example, an API may be secure when handling JSON data but susceptible to injection attacks when dealing with XML.

To change the content type, modify the<span style="color:rgb(255, 192, 0)"> `Content-Type`</span> header, the<span style="color:rgb(255, 192, 0)">n reformat the request body accordingly</span>. You can use the Content type converter BApp to automatically convert data submitted within requests between XML and JSON.


## Using Intruder to find hidden endpoints

Once you have identified some initial API endpoints, you can use Intruder to uncover hidden endpoints. For example, consider a scenario where you have identified the following API endpoint for updating user information:

`PUT /api/user/update`

To identify hidden endpoints, you could use Burp Intruder to find other resources with the same structure. For example, you could add a <span style="color:rgb(255, 192, 0)">payload</span> to the `/update` position of the path with a list of other common functions, such as `delete` and `add`.

When looking for hidden endpoints, <span style="color:rgb(255, 192, 0)">use wordlists based on common API naming conventions and industry terms</span>. Make sure you also include terms that are relevant to the application, based on your initial recon.