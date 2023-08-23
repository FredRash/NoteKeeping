Key Files and Directories
- wp-admin [dir]
- wp-content [dir] - IMPORTENT(We can see here plugins and uploads)
- wp-includes [dir] - IMPORTENT (In here is all of the core components and things used to run WordPress)
- wp-config.php - IMPORTENT (There are hard-coded credentials in here)
- index.php
- license.txt
- readme.html
- wp-activate.php
- wp-blog-header.php
- wp-comments-post.php
- wp-config-sample.php
- wp-cron.php
- wp-links-opml.php
- wp-load.php
- wp-login.php
- wp-mail.php
- wp-settings.php
- wp-signup.php
- wp-trackback.php
- xmlrpc.php

Basic Enumeration
* Get WordPress version in the source code of the page(Can be found in the CSS file also)
* In old versions of WordPress we can go to the /wp-content/plugins directory to find plugins
* Use gobuster to find hidden directories with the /wp-content/plugins
* Use wpscan --url [URL HERE] (Can be used with a web token). Gives a lot of info
* Find usernames!

wpscan
* wpscan --url [URL HERE] 
* wpscan --url [URL HERE]  -U -P [Wordlist HERE] - Password attack

  