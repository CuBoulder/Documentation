# buff.link

buff.link is the url for our url shortener. It lives on `cuw08.colorado.edu`. The domain registrar used for is Ghandi. Our team does not directly manage the domain registry. The DNS registration was last renewed on October, 22, 2024 for a year. If there is an issue loading the site around a year after this date make sure it is renewed.

To access and make changes to the application you will need a couple of things:

- Cisco AnyConnect Secure Mobility Client to access the university's VPN. Go [here](https://oit.colorado.edu/services/network-internet-services/vpn/help/cisco-vpn) to set it up.
- an Identikey account with a secondary sudo account. Go [here](https://oit.colorado.edu/tutorial/identikey-manager-activate-and-manage-your-secondary-account) to set that up.

Once you have those set up you should be able to connect via ssh:
- `ssh YOUR_IDENTIKEY@cuw08.colorado.edu`
- use your identikey password to sign in
- the site's code lives at `/usr/share/nginx/html/url_shortener`

## some common issues

1. We sometimes get permissions issues when the site tries to add files etc to the `sites/default` directory and other directory.
    - correct this by checking the selinux current mode:
        - type `sestatus` and check the 'Current mode' property.
        - If it is listed as enforcing change it to permissive by typing `sudo setenforce 0` and use your secondary sudo account's password when asked for your sudo password.

## perform drupal updates