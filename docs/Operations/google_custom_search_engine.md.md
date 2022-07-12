# Goole Custom Search Engine

All express sites have the ability to add search functionality using google's search engine. By default, the search functionality works of of everything found on www.colorado.edu, which google indexes. 

However, each site can have a custom search engine for finding content only on itself. For example, the search functionality can be configured to only look for content published on www.colorado.edu/YOUR_WEBSITE.

To do this the site owner must initiate a site search request. We get these requests through [Help Scout](https://secure.helpscout.net/). In order to access that you will need an account there and sign in with your credentials.

## Set up a new CSE

### got to [programmable search](https://cse.google.com/cse/all) console

- sign in with websupport@colorado.edu username and password (password is found in KeePassXC osrWeb.kbdx database)
- click "New Search Engine" found on left sidebar
- set "Site to search" to Colorado.edu/PathOfSiteToSearch
- set "name of the search engine" to Colorado.edu/PathOfSiteToSearch
- click "create"
- See Message: "Congratulations! You've successfully created your Custom search engine"
- Click button "Control Panel"
- Copy the Search engine ID for later
- Click Users tab
- Add a user to your custom search engine: mcappaccess@colorado.edu as an administrator. (This step is needed to get ad-free search)
- Create a ServiceNow ticket for the Messaging and Collaboration team using HelpScout to email help@colorado.edu
  - To send email from HelpScout: Change Customer to IT Service Center. Click the "Reply" icon in the upper left. Compose email and send. Keep the ticket open; HelpScout will close it when email is sent.
>
>
> M&C Team: Google CSE for Web Express
> For the Messaging and Collaboration team. The WebExpress Team is updating the Google CSE for the sites that we maintain.
>
>mcappaccess@colorado.edu should have received an email invitation from noreply@google.com, for the custom search engine “www.colorado.edu/MySitePath”.
>
> Please accept it by following the link in the invitation, and choose 'Include me as an Administrator' in the subsequent dialogue box.
>
> Thank you,
> Web Express Team
>

### go to [search console](https://search.google.com/search-console?hl=en&utm_source=wmx&utm_medium=deprecation-pane&utm_content=home&resource_id=https://www.colorado.edu/)

- you have to be authenticated as websupport@colorado.edu
  - click "Settings" down towords the bottom of left sidebar
  - click "ownership verification" and do what you need to do
- click "Sitemaps" in the left sidebar
- add a new sitemap by typing the site's path + "/sitemap.xml" and submit it.
- click url inspection in the left sidebar
- type in the path of the site we are setting up
- when the page loads click "request indexing"

### settings.php file

- clone the site's codebase (On Pantheon)
- update value of the variable "$conf["google_cse_cx"]" to the Search engine ID you copied earlier.
- add, commit, and push the code back up to master (on Pantheon)

## That is it

The site should get search results as soon as google finishes indexing the site. These results will contain adds until the mcappaccess@colorado.edu user is verified. 

## TODOS

It would be nice to know who actually verifies the mcappaccess@colorado.edu user and maybe gain some control over that process ourselves.

Refine the setup steps with some automation. Do the dashboards mentioned above offer api's?
