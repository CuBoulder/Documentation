Recently I tried to launch the ce.colorado.edu site on Pantheon with the help of OIT's DNS changes. However, after their changes the site was still not loading. The message below is Pantheon's response to the ticket I opened for help. 

```
Dan Ficker (Pantheon) 
Jun 17, 2024, 10:03 AM PDT 
Alan,

Here's what I know. When you add a domain to a site, it will not immediately have a certificate once you point DNS to Pantheon. To help with this, we allow you to "validate" ownership of this domain by adding a DNS TXT record or uploading a file to your current host for that domain. If you move DNS A/AAAA records to point to Pantheon before you do that, it may take a few hours or more before DNS propagates and our systems are able to issue a certificate with our provider, Let's Encrypt.

I'm not exactly sure what happened, but it seems like you may have skipped that verification step to get a working certificate before you launch this site. Once you submitted the ticket, I took a look and may have been able to expedite the issuing of the certificate since DNS was pointing to Pantheon, but it's likely it would've happened in a few hours even if I had not helped.

Does that make sense? Any questions?

Thanks for contacting Pantheon Support. And congratulations on the launch of the site on Pantheon.
Dan Ficker
Staff Customer Success Engineer | Pantheon
```
