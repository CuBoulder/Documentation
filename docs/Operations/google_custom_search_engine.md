# Google Custom Search Engine

All express sites have the ability to add search functionality using google's search engine. By default, the search functionality works of of everything found on www.colorado.edu, which google indexes.

However, each site can have a custom search engine for finding content only on itself. For example, the search functionality can be configured to only look for content published on www.colorado.edu/YOUR_WEBSITE.

To do this the site owner must initiate a site search request. We get these requests through [Help Scout](https://secure.helpscout.net/). In order to access that you will need an account there and sign in with your credentials.

## Set up a new CSE

### got to [programmable search](https://cse.google.com/cse/all) console

This documentation uses the 'new Control Panel'. If you are using the 'legacy Control Panel' please make the switch to the new one.

- sign in with websupport@colorado.edu username and password (password is found in KeePassXC osrWeb.kbdx database)
- click "Add"
- in "Name your search engine" set search engine name to "Colorado.edu/PathOfSiteToSearch"
- in "What to Search?" set "enter a site or pages" to "Colorado.edu/PathOfSiteToSearch" and click "create"
    - make sure "Search specific sites or pages" is selected
- click "Add"
- See confirmation that your new search engine has been created
- Click "Customize"
- Copy the Search engine ID for later
- Click on Look and Feel -> All Look and Feel Settings
    - make sure that 'Results only' is selected as a layout
    - click Overview in the left sidebar to return to programmanble search settings
- Click Members in left sidebar
- Add a member to your custom search engine: mcappaccess@colorado.edu as an administrator. (This step is needed to get ad-free search)
- Click on Search Features->Advanced Settings tab in the left sidebar
- Click on Web Search settings and set "Query parameter name" to "cse
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

### add property (for new sub-domain sites only) and verify it

Subdomain sites need their own property added since they are not stacked onto colorado.edu

- Click the drop-down menu in the top left corner, just onder the 'Google Search Console' title and icon.
- click 'add property'
- enter the subdomain + domain (SUBDOMAIN.colorado.edu) to the 'Domain' option and click continue
- to verify ownership of the domain:
    - copy the text record that needs to be added to DNS settings
    - open up a ticket with [OIT Service Now](https://colorado.service-now.com/sncms/dashboard.do) and write that you need to add the copied text record to the site's DNS settings.
    - the property should automatically verify itself in the console when OIT has completed the DNS changes.

### settings for all sites

- select the property (www.colorado.edu for all stacked sites or the subdomain added as detailed above) from the drop-down list just below 'Google Search Console' title
- you must be authenticated as websupport@colorado.edu
  - click "Settings" down towards the bottom of left sidebar
  - click "ownership verification" and do what you need to do
- click "Sitemaps" in the left sidebar
- add a new sitemap by typing the site's path + "/sitemap.xml" and submit it.
- click url inspection in the left sidebar
- type in the path of the site we are setting up
- when the page loads click "request indexing"

### settings.php file (D7 only)

- clone the site's codebase (On Pantheon)
- update value of the variable "$conf["google_cse_cx"]" to the Search engine ID you copied earlier.
- add, commit, and push the code back up to master (on Pantheon)


## Final steps

### D10

- log into a site and go to `/admin/config/search/pages`
- scroll down to the search pages section and add a new search type and select 'Google Programmable Search' from the dropdown
- in the new search edit page:
    - add `results` to the Path form field
    - add the Search engine ID in the 'Google Programmable Search Engine ID' form field
    - save the changes
- in the search pages section make sure the new 'Google Programmable Search' page is set to the default search by selecting the drop down arrow next to the 'Edit' button
- in the search pages section disable the newly non-default 'Content' search by selecting the dropdown arrow next to the 'Edit' button
- click 'Save Configuration' for good measure
- go to `/admin/config/cu-boulder/general` and click the 'Advanced' section
    - select 'this site' under 'Enable searching' section
    - add '/search/results' to Search Page form field
    - click 'Save Configuration' at the bottom of the page

### D7

The site owner, or one of us, needs to log into the site and make sure the search functionality is set to search this site.

go to -> admin/settings/search/search-settings on the site and make the desired settings and then save them.

## That is it

The site should get search results as soon as google finishes indexing the site. These results will contain adds until the mcappaccess@colorado.edu user is verified.

## TODOS

It would be nice to know who actually verifies the mcappaccess@colorado.edu user and maybe gain some control over that process ourselves.

Refine the setup steps with some automation. Do the dashboards mentioned above offer api's?
`
