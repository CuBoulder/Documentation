# Web Express Unique Sites 

There are a handfule of Web Express sites that require unique functionality that applies only to that one site.  Generally these sites have a custom module that is part of the Web Express codebase but that module will only be enabled on that one site.  These unique sites are ennumerated below. 

## Map

Site URL : https://www.colorado.edu/map
Custom Module : https://github.com/CuBoulder/ucb_campus_map  

The campus map integrates with a third-party service, Concept3D to provide a map of the facilites and location on the Main Campus, East Campus and Williams Village. 

## Today

Site URL : https://www.colorado.edu/today
Custom Module : https://github.com/CuBoulder/ucb_article_syndication 

The CU Boulder Today site is the main campus news site.  Content from this site is often syndicated to other Web Express sites.  To facilitate this there are additional taxonomies that allow sites pulling in articles from Today to filter the content being displayed by audience.  The custom module extends the Article node type to add these.  

## FixIt

Site URL : https://fixit.colorado.edu 
Custom Module : https://github.com/CuBoulder/ucb_tma_interface 

The FixIt website is used by on-campus resisdents to enter work orders for repairs to facilites owned and operated by CU Boulder.  They utilize a custom ticketing system known as TMA and these additional modules act as middleware to take the output for form submissions on the sites and submit them to the TMA back-end via and API.  Additionally there are form elements that are populated by the data coming from that TMA back end (e.g. build name and room nummber for those buildings).  

## Bulletin 
Site URL : https://www.colorado.edu/bulletin 
Custom Module : https://github.com/CuBoulder/ucb_subtonode 

The Bulletin website is a place where the CU Boulder community can submit information that may be of more general information to others in the community.  This works by allowing authenticated users to fill out a webform submission.  Site Managers on the site can approve or reject these submissions and when a submission is accepted a custom module turns that submission into a node to be displayed on the main page view of this content.  
