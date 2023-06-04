* site - Tells google to show you results from a certain site only.
example: print site:python.org
searches the key world print in python.org site

* inurl - Searches for pages with URL that match the search string.
example: inurl:"/course/jupto.php" site:example

* intitle -  Finds specific strings in a page's title.
example: initile:"index of" site:example.com

* link - searches for web pages that contain links to a specified URL.
example: link:"https://en.wikipedia.org/wiki/Redos".

* filetype - Searches for pages with a specific file extension.
example: filetype:log site:example.com

* query for subdomines - site:*.example.com

* Kibana dashboard query - site:example.com inurl:app/kibana

* Amazon s3 servers query - site:s3.amazonaws.com COMPANY_NAME

* script to find sensitive files - site: example.com ext:php (can also be: log,cfm,.jsp and .pl)

* Combine search terms for more accurate search - site:example.com ext:txt password.
Searches the site example.com for text files that contain password.
