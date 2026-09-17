# Trust & Syndication

Trust and Syndication is a new add-on for Web Express which allows for the discovery of trusted content and the syndication of that content across sites within the Web Express service.  

The Discovery sites is here : https://www.colorado.edu/trust/discovery/ 


## Trust 
Individual sites within the Web Express ecosystem can be tagged as a `trusted` site.  Sites tagged this way will be scanned by the discovery site to find content that is allowed to be syndicated.  Additional information about adding trusted content can be found here : https://github.com/CuBoulder/ucb_trust_schema 


## Syndication 
The discovery site will scan every Web Express site that has been tagged as a trusted source.  Content that is syndicated from thost trusted sites will be presented on the discovery site to facilitate other Web Express finding this syndicatable content and then embedding that content on their own sites.  Additional information about the syndication module can be found here : https://github.com/CuBoulder/ucb_trusted_content_discovery

## Goal of the Trust and Syndication System 
One of the problems with having a thousand sites for a single university is that there are many sites that want to have content for their own audiences that comes from other sites.  e.g health, parking, registration information.  This leads to the duplication of content on sites.  The duplication of content across several sites causes several web-specific problems.  Because sites are copying content for which they are not the primary SME they are less likely to notice when changes to this content is warranted or necessary.  Additionaly by having multiple instances of the same content on many sites this causes difficulty for traditional and agentic search engines to find the authoritative source of that information.  

The Trust and Syndication system solves these issues by allowing the content to exist at the authoritative source but still be displayed on additional sites.  Since this is embedded on the client side it won't pollute the search space and because it is pulled in dynamically, when the content is updated by the authoritative source any subscribed sites will automatically get the updated version of that content.  

## Future Updates 
The Trust and Syndication is currently in an open beta phase of testing.  Plans for future expansions include the ability to have notification channels which work in both direction.  One channel would allow for sites utilizing subscribed content to be made aware when content is updated that they are subscribed to.  The other direction would allow site owners to notify trusted sources of issues with their content or request additional features for content they are sharing.  

